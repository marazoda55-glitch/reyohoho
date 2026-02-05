<template>
  <div class="movie-info">
    <div class="content">
      <div id="kinobox_player" style="width: 100%; height: 550px; background: #000; margin-top: 20px;"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MovieInfo',
  mounted() {
    // Создаем и запускаем скрипт плеера прямо здесь
    const script = document.createElement('script');
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
