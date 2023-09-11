<template>
  <div>
    result: {{ result }}
    <br />
    pending: {{ p }}
    <br />
    error: {{ e }}
    <button @click="getData">fetch</button>
  </div>
</template>
<script setup>
const result = ref()
const p = ref()
const e = ref()
const getData = async () => {
  try {
    const { data, pending, error, refresh } = await useAsyncData(
      'data',
      () => $fetch('/api/get-data')
    )
    result.value = data.value
    p.value = pending.value
    e.value = error.value
    console.log(data.value)
  } catch (error) {
    e.value = error.message
  }
}
</script>