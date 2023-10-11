<script setup>
const route = useRoute()

const { data, error } = await useFetch(
    `https://httpbin.org/status/500`,
    {
      pick: ["Plot", "Title", "Error"],
      key: `/movies/${route.params.id}`
    })
if (error.value) {
  showError({statusCode: 500, statusMessage: "Ops"})
}
if (data?.value?.Error === "Incorrect IMDb ID.") {
  showError({statusCode: 404, statusMessage: "Page Not Found"})
}

// const { data } = useAsyncData(`/movie/${route.params.id}`,() => {
//   return $fetch(`http://www.omdbapi.com/?apiKey=8e3f600b&i=${route.params.id}`)
// }, {
//   pick: ["Plot", "Title"],
// })
</script>

<template>
  <div>
    <pre>
      {{ data }}
    </pre>
  </div>
</template>

<style scoped></style>
