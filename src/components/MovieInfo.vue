<template>
  <div class="movie-info">
    <div class="content">
       <PlayerComponent :id="$route.params.id" />
    </div>
  </div>
</template>

<script>
import PlayerComponent from './PlayerComponent.vue';
export default {
  name: 'MovieInfo',
  components: { PlayerComponent }
}
</script>
