## nextTick()

**nextTick()** is called when the vue dom is ready like **onMounted** lifecycle hook. Here is a simple carousel code example
```js
<script setup>
import { ref, onBeforeMount, onMounted, nextTick} from 'vue'
let carousel = null
const newItem = ref("https://plus.unsplash.com/premium_photo-1688821128189-c4f2d10b33f1?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D")

onMounted(() => {
  const carouselDiv = document.getElementById('carousel')
  carousel = new Flickity(carouselDiv)
})

const sources = ref([
    "https://images.pexels.com/photos/19882695/pexels-photo-19882695/free-photo-of-concrete-breakers-on-the-sea-coast.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1",
    "https://images.pexels.com/photos/19737271/pexels-photo-19737271/free-photo-of-view-of-a-lake-in-mountains.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1",
    "https://images.pexels.com/photos/19896963/pexels-photo-19896963/free-photo-of-yllas-lapland.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1",
    "https://images.pexels.com/photos/20436787/pexels-photo-20436787/free-photo-of-a-snow-capped-mountain-is-seen-at-dusk.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1",
    "https://images.pexels.com/photos/19606362/pexels-photo-19606362/free-photo-of-blurred-photo-of-a-beach-at-dusk.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1"
])

const addItem = () => {
  const carouselDiv = document.getElementById('carousel')
  sources.value.push(newItem.value)
  carousel.destroy()
  nextTick(() => {
    carousel = new Flickity(carouselDiv)
  })
}
</script>
```