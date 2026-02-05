<template>
  <div class="player-container">
    <div id="kinobox_player" style="width: 100%; height: 550px; background: #000;"></div>
  </div>
</template>

<script>
export default {
  name: 'PlayerComponent',
  props: ['id'],
  mounted() {
    this.initKinobox();
  },
  methods: {
    initKinobox() {
      const script = document.createElement('script');
      script.src = 'https://kinobox.tv/static/kinobox.min.js';
      script.async = true;
      script.onload = () => {
        if (window.Kinobox) {
          new window.Kinobox('#kinobox_player', {
            search: { kinopoisk: this.id || location.href.split('/').pop() },
            menu: { enable: true, default: 'Просмотр' }
          }).init();
        }
      };
      document.head.appendChild(script);
    }
  }
}
</script>
