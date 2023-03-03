/* eslint-disable */
<template>
  <div class="reviews-slider">
    <ul>
      <li v-for="(item, index) in items" :key="index" :class="{ active: activeIndex === index }">
        {{ item.name }}
      </li>
    </ul>
    <ul>
      <li v-for="(item, index) in items" :key="index" class="indicator-dot" :class="{active: activeIndex === index }">
        dot
      </li>
    </ul>
    <div class="controls">
      <button @click="prev">&lt;</button>
      <button @click="next">&gt;</button>
    </div>
    <div class="indicators">
      <span v-for="(item, index) in items" :key="index" :class="{ active: activeIndex === index }" @click="setActive(index)"></span>
    </div>
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue';



export default {
  setup() {

    const reviewsData = [ 
        { photo: 'https://ay.solverstaging.dev/media/wysiwyg/person-1.jpg',
          name: 'Nicolas Reyes',
          message: 'Pizza ipsum dolor amet garlic extra sauce chicken wing party thin crust stuffed. Sausage hawaiian pineapple, fresh tomatoes garlic broccoli bbq pizza ranch bbq sauce sausage. Bbq sauce white garlic pineapple sauteed onions, mayo peppers chicken wing buffalo sauce bacon & tomato meatball lasagna thin crust. Melted cheese stuffed thin crust fresh tomatoes extra cheese.'
        },
        { photo: 'https://ay.solverstaging.dev/media/wysiwyg/person-2.jpg',
          name: 'Chico Bouchikhi',
          message: 'Fresh tomatoes garlic broccoli bbq pizza ranch bbq sauce sausage. Bbq sauce white garlic pineapple sauteed onions, mayo peppers chicken wing buffalo sauce bacon & tomato meatball lasagna thin crust. Melted cheese stuffed thin crust fresh tomatoes extra cheese.'
        },
        { photo: 'https://ay.solverstaging.dev/media/wysiwyg/person-3.jpg',
          name: 'Tonino Baliardo',
          message: 'Melted cheese stuffed thin crust fresh tomatoes extra cheese. Party garlic parmesan ham pie NY style hand tossed onions garlic large pesto, sauteed onions bacon & tomato.'
        },
      ]

    const items = ref(
      [...reviewsData]
      );
    const activeIndex = ref(0);
    let intervalId;

    const next = () => {
      activeIndex.value = (activeIndex.value + 1) % items.value.length;
    };

    const prev = () => {
      activeIndex.value = (activeIndex.value - 1 + items.value.length) % items.value.length;
    };

    const setActive = (index) => {
      activeIndex.value = index;
    };

    onMounted(() => {
      intervalId = setInterval(() => {
        next();
      }, 5000);

    });

    onUnmounted(() => {
      clearInterval(intervalId);
    });

    return {
      items,
      activeIndex,
      next,
      prev,
      setActive,
    };
  },
};
</script>

<style>
.slider {
  position: relative;
}

.slider ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

.slider li {
  display: none;
  position: absolute;
  top: 0;
  left: 0;
}

.slider li.active {
  display: block;
}

.controls {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
}

.controls button {
  border: none;
  background: none;
  font-size: 1.5rem;
  cursor: pointer;
  margin: 0 0.5rem;
}

.indicators {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  margin: 1rem 0;
}

.indicators span {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background-color: #bbb;
  margin: 0 0.5rem;
  cursor: pointer;
}

.indicators span.active {
  background-color: #333;
}
</style>