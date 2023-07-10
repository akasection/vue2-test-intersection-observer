<template>
  <div class="card" ref="card">
    <p v-if="vis && !visFlag" style="height: 100%">LOADING!!!</p>
    <template v-if="visFlag">
      <p class="title">Title</p>
      <p class="price">Price</p>
      <div class="dummyimg"></div>
      <button class="action">Buy</button>
  </template>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref, watch } from 'vue'
export default defineComponent({
  setup() {
    const obs = ref<IntersectionObserver>()
    const card = ref<HTMLDivElement>()
    const vis = ref(false)
    const visFlag = ref(false)

    onMounted(() => {
      obs.value = new IntersectionObserver(([entry]) => {
        if(!entry.isIntersecting) return
        vis.value = true
        obs.value?.disconnect()
      })
      obs.value.observe(card.value!!)


    })

    watch(vis, (val) => {
      if(!val) return
      setTimeout(() => {
        visFlag.value = true
      }, 1300)
      console.log('yuhu')
    })

    return { obs, card, vis, visFlag }
  }
})
</script>

<style scoped>
.card {
  width: 200px;
  background-color: azure;
  border-color: gray;
  border-width: 1px;
  border-style: solid;
  border-radius: 8px;
  padding: 5px;
  display: flex;
  justify-content: center;
  flex-direction: column;
  position: relative;

}
</style>
