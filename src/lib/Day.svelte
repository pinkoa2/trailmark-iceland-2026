<script>
  import Gallery from './Gallery.svelte'

  let { dayNumber, title, description, mapEmbedUrl = null, noMap = false, photos = [], active = true, onloaded } = $props();
</script>

<section class="day">
  <h2>Day {dayNumber}{title ? `: ${title}` : ''}</h2>

  {#if description}
    <p class="description">{description}</p>
  {/if}

  {#if mapEmbedUrl}
    <div class="map">
      <iframe
        src={mapEmbedUrl}
        title="Day {dayNumber} route"
        loading="lazy"
        referrerpolicy="no-referrer-when-downgrade"
      ></iframe>
    </div>
  {:else if !noMap}
    <div class="map map-placeholder">Map coming soon</div>
  {/if}

  <Gallery {photos} {active} {onloaded} />
</section>

<style>
  .day {
    padding: 32px 16px;
    max-width: 960px;
    margin: 0 auto;
  }

  h2 {
    font-size: clamp(1.5rem, 4vw, 2rem);
    margin-bottom: 12px;
  }

  .description {
    margin-bottom: 20px;
    line-height: 1.6;
  }

  .map {
    width: 100%;
    aspect-ratio: 16 / 9;
    margin-bottom: 20px;
    border-radius: 8px;
    overflow: hidden;
  }

  .map iframe {
    width: 100%;
    height: 100%;
    border: 0;
  }

  .map-placeholder {
    display: flex;
    align-items: center;
    justify-content: center;
    background: var(--code-bg, #f0f0f0);
    color: var(--text, #666);
    font-size: 0.9rem;
  }
</style>
