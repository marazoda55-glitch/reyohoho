<template>
  <div class="player-wrapper">
    <div id="kinobox_player"></div>
  </div>
</template>

<script>
export default {
  props: ['id'],
  watch: {
    // Ждем, пока ID придет из базы данных
    id: {
      handler(newVal) {
        if (newVal) this.loadPlayer(newVal);
      },
      immediate: true
    }
  },
  methods: {
    loadPlayer(kpId) {
      // Очищаем контейнер перед новой загрузкой
      const container = document.getElementById('kinobox_player');
      if (container) container.innerHTML = '';

      const script = document.createElement('script');
      script.src = 'https://kinobox.tv/static/kinobox.min.js';
      script.async = true;
      script.onload = () => {
        if (window.Kinobox) {
          new window.Kinobox('#kinobox_player', {
            search: { kinopoisk: kpId },
            menu: { enable: true, default: 'Просмотр' }
          }).init();
        }
      };
      document.head.appendChild(script);
    }
  }
}
</script>

<style scoped>
.player-wrapper {
  width: 100%;
  min-height: 500px;
  background: #000;
  border-radius: 12px;
  margin: 20px 0;
}
</style>
