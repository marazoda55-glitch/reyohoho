<template>
  <div id="kinobox_player" style="width: 100%; height: 550px; background: #000;"></div>
</template>

<script>
export default {
  props: ['id'],
  mounted() {
    const script = document.createElement('script');
    script.src = 'https://kinobox.tv/static/kinobox.min.js';
    script.async = true;
    script.onload = () => {
      if (window.Kinobox) {
        new window.Kinobox('#kinobox_player', {
          search: { kinopoisk: this.id || location.href.split('/').pop() }
        }).init();
      }
    };
    document.head.appendChild(script);
  }
}
</script>
