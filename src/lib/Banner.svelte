<script>
  let { title, src = null, alt = '' } = $props();
</script>

<header class="banner">
  {#if src}
    <img class="banner-bg" {src} alt="" aria-hidden="true" />
    <img class="banner-image" {src} {alt} />
  {:else}
    <div class="banner-placeholder" aria-hidden="true"></div>
  {/if}
  <div class="banner-overlay" aria-hidden="true"></div>
  <h1>{title}</h1>
</header>

<style>
  .banner {
    position: relative;
    width: 100%;
    height: 60vh;
    min-height: 320px;
    max-height: 560px;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }

  .banner-bg {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    filter: blur(24px) brightness(0.8);
    transform: scale(1.1);
  }

  .banner-image {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    object-fit: contain;
  }

  .banner-placeholder {
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, #1b3a4b 0%, #2f6690 50%, #a7c7d9 100%);
  }

  .banner-overlay {
    position: absolute;
    inset: 0;
    background: rgba(0, 0, 0, 0.25);
  }

  h1 {
    position: relative;
    z-index: 1;
    color: #fff;
    text-align: center;
    font-size: clamp(1.5rem, 4vw, 2.5rem);
    font-weight: 600;
    letter-spacing: -0.02em;
    text-shadow: 0 2px 12px rgba(0, 0, 0, 0.35);
    max-width: min(80%, 600px);
    margin: 0 auto;
    padding: 0 1.5rem;
    box-sizing: border-box;
  }
</style>
