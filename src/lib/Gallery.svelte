<script>
  let { photos = [], active = true, onloaded } = $props();
  let activeIndex = $state(null);
  let loadedCount = $state(0);
  let notified = $state(false);
  let allLoaded = $derived(photos.length === 0 || loadedCount >= photos.length);

  function isVideo(src) {
    return /\.(mp4|mov|webm|m4v)$/i.test(src);
  }

  function trackLoad(node) {
    const done = () => {
      loadedCount += 1;
    };
    if (node.complete) done();
    else {
      node.addEventListener('load', done);
      node.addEventListener('error', done);
    }
    return {
      destroy() {
        node.removeEventListener('load', done);
        node.removeEventListener('error', done);
      },
    };
  }

  $effect(() => {
    if (active && allLoaded && !notified) {
      notified = true;
      onloaded?.();
    }
  });

  function open(index) {
    activeIndex = index;
  }
  function close() {
    activeIndex = null;
  }
  function next(e) {
    e?.stopPropagation();
    if (activeIndex === null) return;
    activeIndex = (activeIndex + 1) % photos.length;
  }
  function prev(e) {
    e?.stopPropagation();
    if (activeIndex === null) return;
    activeIndex = (activeIndex - 1 + photos.length) % photos.length;
  }
  function onKeydown(e) {
    if (activeIndex === null) return;
    if (e.key === 'Escape') close();
    else if (e.key === 'ArrowRight') next();
    else if (e.key === 'ArrowLeft') prev();
  }
</script>

<svelte:window onkeydown={onKeydown} />

<div class="gallery-wrapper">
  <div class="gallery" class:loaded={allLoaded}>
    {#each photos as photo, i (photo.src)}
      <figure class="gallery-item">
        <button type="button" class="thumb" onclick={() => open(i)} aria-label="View {isVideo(photo.src) ? 'video' : 'photo'} full size">
          {#if active}
            {#if isVideo(photo.src)}
              <img src={photo.poster} alt={photo.alt ?? ''} use:trackLoad />
              <span class="play-badge" aria-hidden="true"></span>
            {:else}
              <img src={photo.src} alt={photo.alt ?? ''} use:trackLoad />
            {/if}
          {/if}
        </button>
        {#if photo.caption}
          <figcaption>{photo.caption}</figcaption>
        {/if}
      </figure>
    {/each}
  </div>

  {#if !allLoaded}
    <div class="gallery-loading" aria-hidden="true">
      <div class="spinner"></div>
      <span>Loading...</span>
    </div>
  {/if}
</div>

{#if activeIndex !== null}
  <div
    class="lightbox"
    role="dialog"
    aria-modal="true"
    tabindex="-1"
    onclick={(e) => { if (e.target === e.currentTarget) close(); }}
    onkeydown={onKeydown}
  >
    <button class="lightbox-close" type="button" onclick={close} aria-label="Close">&times;</button>

    {#if photos.length > 1}
      <button class="lightbox-nav prev" type="button" onclick={prev} aria-label="Previous photo">&#8249;</button>
    {/if}

    <figure class="lightbox-figure">
      {#if isVideo(photos[activeIndex].src)}
        <!-- svelte-ignore a11y_media_has_caption -->
        <video
          class="lightbox-image"
          src={photos[activeIndex].src}
          poster={photos[activeIndex].poster}
          controls
          autoplay
          playsinline
        ></video>
      {:else}
        <img
          class="lightbox-image"
          src={photos[activeIndex].src}
          alt={photos[activeIndex].alt ?? ''}
        />
      {/if}
      {#if photos[activeIndex].caption}
        <figcaption class="lightbox-caption">{photos[activeIndex].caption}</figcaption>
      {/if}
    </figure>

    {#if photos.length > 1}
      <button class="lightbox-nav next" type="button" onclick={next} aria-label="Next photo">&#8250;</button>
    {/if}
  </div>
{/if}

<style>
  .gallery-wrapper {
    position: relative;
  }

  .gallery {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 8px;
    opacity: 0;
    transition: opacity 0.3s ease;
  }

  .gallery.loaded {
    opacity: 1;
  }

  @media (min-width: 640px) {
    .gallery {
      grid-template-columns: repeat(2, 1fr);
      gap: 12px;
    }
  }

  .gallery-loading {
    position: absolute;
    inset: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 12px;
    min-height: 160px;
    color: var(--text, #666);
    font-size: 0.9rem;
  }

  .spinner {
    width: 32px;
    height: 32px;
    border: 3px solid var(--code-bg, #e0e0e0);
    border-top-color: var(--text, #666);
    border-radius: 50%;
    animation: spin 0.8s linear infinite;
  }

  @keyframes spin {
    to {
      transform: rotate(360deg);
    }
  }

  .gallery-item {
    margin: 0;
  }

  .gallery-item .thumb {
    all: unset;
    position: relative;
    display: flex;
    align-items: flex-end;
    justify-content: center;
    width: 100%;
    aspect-ratio: 1 / 1;
    overflow: hidden;
    border-radius: 16px;
    background: transparent;
    cursor: pointer;
  }

  .gallery-item img {
    max-width: 100%;
    max-height: 100%;
    width: auto;
    height: auto;
    object-fit: contain;
    display: block;
    border-radius: 16px;
  }

  .play-badge {
    position: absolute;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    pointer-events: none;
  }

  .play-badge::after {
    content: '';
    position: absolute;
    inset: 0;
    background: rgba(0, 0, 0, 0.15);
  }

  .play-badge::before {
    content: '\25B6';
    position: relative;
    z-index: 1;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 48px;
    height: 48px;
    border-radius: 50%;
    background: rgba(0, 0, 0, 0.5);
    color: #fff;
    font-size: 1.2rem;
    padding-left: 4px;
    box-sizing: border-box;
  }

  .gallery-item figcaption {
    margin-top: 4px;
    font-size: 0.7rem;
    font-style: italic;
    color: var(--text, #666);
    text-align: center;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .lightbox {
    position: fixed;
    inset: 0;
    background: rgba(0, 0, 0, 0.55);
    backdrop-filter: blur(6px);
    -webkit-backdrop-filter: blur(6px);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000;
    padding: 16px;
  }

  .lightbox-figure {
    margin: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    max-width: 100%;
    max-height: 100%;
  }

  .lightbox-image {
    max-width: 100%;
    max-height: 85vh;
    object-fit: contain;
    border-radius: 4px;
  }

  .lightbox-caption {
    margin-top: 12px;
    color: #fff;
    font-size: 0.9rem;
    font-style: italic;
    text-align: center;
    text-shadow: 0 1px 4px rgba(0, 0, 0, 0.5);
  }

  .lightbox-close,
  .lightbox-nav {
    position: absolute;
    background: none;
    border: none;
    color: #fff;
    cursor: pointer;
    line-height: 1;
  }

  .lightbox-close {
    top: 12px;
    right: 12px;
    font-size: 2rem;
    padding: 8px;
  }

  .lightbox-nav {
    top: 50%;
    transform: translateY(-50%);
    font-size: 2.5rem;
    padding: 8px 16px;
  }

  .lightbox-nav.prev {
    left: 4px;
  }

  .lightbox-nav.next {
    right: 4px;
  }
</style>
