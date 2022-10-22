<template>
  <div class="home">
    <!-- <p ref="p">My name is {{name}} and my age is {{age}}</p>
    <button @click="handleClick">click me</button>
    <button @click="age++">add 1 to age</button>
    <input type="text" v-model="name"> -->

    <h1>Home</h1>
    <!-- <h2>Refs</h2>
    <p>{{ ninjaOne.name}} - {{ninjaOne.age}} - {{nameOne}}</p>
    <button @click="updateNinjaOne">Update ninja one </button>

    <h2>Reactive</h2>
    <p>{{ninjaTwo.name}} - {{ninjaTwo.age}}</p>
    <button @click="updateNinjaTwo">Update ninja two </button> -->
    <input type="text" v-model="search">
    <p>search term - {{search}}</p>
    <div v-for="name in matchName" :key="name">
      <p>{{name}}</p>
    </div>
    <button @click="handleClick">stop watching</button>
  </div>
</template>

<script>
// @ is an alias to /src

import { computed } from '@vue/reactivity';
import { watch, watchEffect } from 'vue';
import { ref, reactive } from 'vue'

export default {
  name: 'HomeView',
  setup(){
    // console.log(this)

    // const p = ref(null)

    // const name = ref('mario')
    // const age = ref(30)

    // const handleClick = () =>{
    //   name.value = 'luigi';
    //   age.value ='35'
    // }

    // return { name, age, handleClick, p}

    // const ninjaOne = ref({name : 'mario', age: 30})
    // const ninjaTwo = reactive({name: 'luigi', age: 35})

    // const nameOne = ref('Lionel')

    // const updateNinjaOne = () => {
    //   ninjaOne.value.age = 40;
    //   nameOne.value = "Cheryl"
    // }

    // const updateNinjaTwo = () => {
    //   return ninjaTwo.age = 95
  
    // }

    // return {ninjaOne, updateNinjaOne, ninjaTwo, updateNinjaTwo, nameOne}
    const search = ref('')
    const names = ref(['gabriel', 'chiyan', 'kaizer', 'cheryl'])

    const stopWatch = watch(search, () => {
      console.log('watch function ran')
    })

    const stopEffect = watchEffect(() => {
      console.log('watchEffect function ran', search.value)
    })

    const handleClick = (() => {
      stopWatch()
      stopEffect()
    })

    const matchName = computed(() => {
      return names.value.filter( (name) => name.includes(search.value))
    })
    return {names, search, matchName, stopWatch, stopEffect, handleClick }
  },
  
}
</script>
