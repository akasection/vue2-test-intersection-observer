<template>
  <div id="app">
    <img src="./assets/logo.svg" alt="Vite logo" />
    <HelloWorld msg="Hello Vue 2 + Vite" />
    <hr style="margin-bottom: 500px;">
    <div ref="tobat"></div>
    <Intersect @enter="showPanel">
      <div class="intersect-container">
        <div class="intr" v-show="disp">
          <Hide v-for="_ in 3"></Hide>
        </div>
      </div>
    </Intersect>
    <br>
    <hr>
    <p>
      Essentially, decorators can be used to metaprogram and add functionality to a value, without fundamentally changing its external behavior.

      This proposal differs from previous iterations where decorators could replace the decorated value with a completely different type of value. The requirement for decorators to only replace a value with one that has the same semantics as the original value fulfills two major design goals:

      It should be easy both to use decorators and to write your own decorators. Previous iterations such as the static decorators proposal were complicated for authors and implementers in particular. In this proposal, decorators are plain functions, and are accessible and easy to write.
      Decorators should affect the thing they're decorating, and avoid confusing/non-local effects. Previously, decorators could change the decorated value in unpredictable ways, and also add completely new values which were unrelated. This was problematic both for runtimes, since it meant decorated values could not be analyzed statically, and for developers, since decorated values could turn into completely different types of values without any indicator to the user.
    </p>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, /*onMounted*/ } from 'vue'
import HelloWorld from './components/HelloWorld.vue'
import Hide from './components/Hide.vue'
import Intersect from 'vue-intersect'

export default defineComponent({
  name: 'App',
  components: {
    HelloWorld,
    Hide,
    Intersect
  },
  setup() {
    const disp = ref(false)
    const tobat = ref<HTMLDivElement>()
    // const obs = ref<IntersectionObserver>()

    function showPanel() {
      disp.value = true
    }

    // onMounted(() => {
    //   obs.value = new IntersectionObserver(([entry]) => {
    //   if (!entry.isIntersecting) return
    //   disp.value = true
    //   console.log(entry, 'updated')
    // }, {
    //   root: null,
    //   threshold: [0, 0.2],
    //   rootmargin: '0px 0px 0px 0px',
    // })
    // obs.value.observe(tobat.value!!)
    // })

    return { disp, showPanel, tobat }
  },
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  width: 100%;
}
.intr {
  width: 80%;
  margin: auto;
  display: flex;
  gap: 4px;
  justify-content: center;
}
</style>
