<template>
<ul>
  <li :class="{active: modelValue === 'poor'}"><button type="button" @click="activate('poor')">Poor</button></li>
  <li :class="{active: modelValue === 'average'}"><button type="button" @click="activate('average')">Average</button></li>
  <li :class="{active: modelValue === 'great'}"><button type="button" @click="activate('great')">Great</button></li>
</ul>
</template>

<script>
export default {
  props: ['modelValue'],
  emits: ['update:modelValue'],
  computed: {
    activeOption() {
      return this.modelValue;
    }
  },
  methods: {
    activate(option) {
      this.$emit('update:modelValue', option);
    }
  }
}
</script>

<style scoped>
.active {
  border-color: darkblue;
  background-color: lightblue;
  color: white;
}

.active-button {
  background-color: darkblue;
  color: white;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0.5rem 0;
  display: flex;
}

li {
  margin: 0 1rem;
  border: 1px solid #ccc;
  padding: 1rem;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 10%;
}

button {
  font: inherit;
  border: none;
  background-color: transparent;
  cursor: pointer;
}

</style>