<template>
  <div class="home">
    <TimerView/>
  </div>
</template>

<script>
// @ is an alias to /src
import TimerView from '@/components/TimerView.vue'

export default {
  name: 'HomeView',
  components: {
    TimerView
  }
}
</script>
