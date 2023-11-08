<template>
  <div :class="`h-40 w-40 border rounded-md ${props.warna}`" @click="handleClick" />
</template>

<script setup>
const props = defineProps({
  warna: {
    default: 'bg-yellow-500'
  }
})

const emit = defineEmits(['onClick'])

const handleClick = () => {
  emit('onClick')
}
</script>
