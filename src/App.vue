<template>
  <Header title="Remember me" />
  <ResourceView></ResourceView>
</template>

<script>
import Header from './components/layouts/Header.vue';
import ResourceView from './components/learning-resource/ResourceView.vue';

export default {
  components: {
    Header,
    ResourceView,
  },
  data() {
    return {
      
    };
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

* {
  box-sizing: border-box;
}

html {
  font-family: 'Roboto', sans-serif;
}

body {
  margin: 0;
}
</style>
