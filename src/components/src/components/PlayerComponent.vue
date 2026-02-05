<template>
  <div style="width:100%; min-height:550px; background:#000; margin:20px 0;">
    <div id="kinobox_player"></div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue'
onMounted(() => {
  const s = document.createElement('script')
  s.src = 'https://kinobox.tv/static/kinobox.min.js'
  s.async = true
  s.onload = () => {
    if (window.Kinobox) {
      new window.Kinobox('#kinobox_player', {
        search: { kinopoisk: window.location.pathname.split('/').pop() }
      }).init()
    }
  }
  document.head.appendChild(s)
})
</script>
