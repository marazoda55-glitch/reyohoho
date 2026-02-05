<template>
  <div class="movie-info">
    <div class="content">
      <div id="kinobox_player" style="width: 100%; height: 550px; background: #000; margin: 20px 0;"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MovieInfo',
  mounted() {
    // Удаляем старые скрипты, если они были
    const oldScript = document.getElementById('kinobox-js');
    if (oldScript) oldScript.remove();

    const script = document.createElement('script');
    script.id = 'kinobox-js';
    script.src = 'https://kinobox.tv/static/kinobox.min.js';
    script.async = true;
    script.onload = () => {
      if (window.Kinobox) {
        new window.Kinobox('#kinobox_player', {
          search: { kinopoisk: this.$route.params.id || location.href.split('/').pop() },
          menu: { enable: true, default: 'Просмотр' }
        }).init();
      }
    };
    document.head.appendChild(script);
  }
}
</script>
