Computed property in vue is a cache base function. When you call computed property that will calculate it's property if anything is changes there, otherwise it will remember the previous value where the regular function is recalculate every time.
```js
<script setup>
import { ref, computed } from 'vue'

const n1 = ref(Number(0))
const n2 = ref(Number(0))

const getTotal = computed(()=>{
    return n1.value + n2.value
})
</script>
```

## get, set in computed
Let's see how the get and set work in computed property
```vue
<script setup>
import { ref, computed } from 'vue'
const fname = ref('John')
const lname = ref('Doe')
const fullName = computed({
    get: () => `${fname.value} ${lname.value}`,
    set: (value) => {
        const [newFname, newLname] = value.split(' ')
        fname.value = newFname
        lname.value = newLname
    }
})
</script>

<template>
    <h2>Compute Get Set</h2>
    <input type="text" v-model="fname"><br>
    <input type="text" v-model="lname">
    <p>Result: {{ fullName }}</p>
    <button @click="fullName = 'Khalid Bin'">Change Name</button>
</template>

<style scoped>

</style>
```