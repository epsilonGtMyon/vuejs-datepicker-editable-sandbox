<template>
  <div>
    <EditableDatePicker v-model="dateValue01" />
  </div>
</template>

<script>
import EditableDatePicker from './components/EditableDatePicker';

export default {
  name: 'app',
  components: {
    EditableDatePicker,
  },
  data(){
    return {
      dateValue01:null,
    }
  }
}
</script>

<style lang="scss">
</style>
