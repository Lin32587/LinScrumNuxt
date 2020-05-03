<template>
  <div class="cc-card">
    <h3>{{ data.title }}</h3>
    <p>
      {{ data.description }}
      <button class="cc-btn" v-if="!data.done" @click="markDone()">
              Mark Done
      </button>
    </p>
  </div>
</template>

<script>
export default {
  name:'dndComponent',
  props:['data'],
  methods:{
    markDone(){
      this.$emit('done',this.data);
    }
  }
}
</script>

<style>

</style>
