<template>
  <v-container>
    <!-- 타블렛 안에는 하나의 컴포넌트만 들어가기때문에 여러개의 컴포넌트를 이용할시 div 안에 만들어준다. -->
    <v-layout>
      <v-flex xs12>
        <Home></Home>
      </v-flex>
    </v-layout>



  </v-container>
</template>

<script>
 import Home from './components/Home.vue'

export default {
    components: {
      Home
    }

}



</script>

