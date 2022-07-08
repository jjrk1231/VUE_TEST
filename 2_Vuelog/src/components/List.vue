<template>
  <div>
    <div v-for="(blog, i) in blogData" :key="i">
      <h5 v-on:click="$router.push('/detail/'+i)">{{ blog.title }}</h5>
      <p>{{ blog.date }}</p>
    </div>
  </div>
</template>

<script>

export default {
  name: "List",
  data() {
    return {

    }
  },
  props: {
    blogData : Array,
  },
}
</script>

<style scoped>

</style>