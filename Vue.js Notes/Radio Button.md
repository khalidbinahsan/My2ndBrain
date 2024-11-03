Look at the example of radio button

This is **App.vue** code
```js
<script setup>
import {ref, reactive} from 'vue'
import Radio from './components/Radio.vue';
const fruit = ref('Apple')
</script>

<template>
  <section class="mt-10">
    <div class="container">
      <div class="flex justify-center">
        <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
        <h2 class="text-2xl">Vue Component</h2>
      </div>
    </div>
  </section>
  <section class="my-10">
    <div class="container">
      <div class="mt-5">
       <Radio label="Apple" value="Apple" v-model="fruit" /><br>
       <Radio label="Mango" value="Mango" v-model="fruit" /><br>
       <Radio label="Lychee" value="Lychee" v-model="fruit" /><br>
      </div>
    </div>
  </section>
</template>

<style scoped>

</style>

```

This is **component.vue** file
```js
<script setup>
import { computed } from 'vue';
const props = defineProps([
   'label', 'modelValue', 'value' 
])
const emit = defineEmits(['update:modelValue'])
const radioValue = computed({
    get: () => props.modelValue,
    set: (value) => emit('update:modelValue', value)
})
</script>

<template>
<input type="radio" :value="value" v-model="radioValue" />
<label class="ml-2">{{ label }}</label>
</template>

<style scoped>

</style>
```