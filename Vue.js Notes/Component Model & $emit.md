Included some example of component model that how can I change the model value from a component as well by using **$emit** 

**FormField.vue** file
```vue
<script setup>
const props = defineProps([
    'label', 'modelValue', 'type'
])
const emit = defineEmits(['modelValue'])
</script>

<template>
<div class="flex flex-col mx-auto max-w-96 my-3">
    <label class="font-bold">{{ label }}</label>
    <input :type="type" :value="modelValue" @input="$emit('update:modelValue', $event.target.value)"  class="border-2 border-blue-400 mt-3 py-2 px-4 rounded">
</div>
</template>

<style scoped>  

</style>
```

**app.vue** file
```vue
<script setup>
import {ref} from 'vue'
import FormField from './components/TextComponent.vue';
const name = ref('John Doe')
const email = ref('johndoe@gmail.com')
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
        <FormField label="Name" type="text" v-model="name" />
        <FormField label="Email" type="email" v-model="email" />
      </div>
    </div>
  </section>
</template>

<style scoped>

</style>
```

The example above we are talking about, how to send data from **app.vue** to **component** through **v-model**
Now we see an another example about how to send data through **object** Let's see.....