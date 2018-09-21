<template>
    <button @click="toggleFavorite(joke, id)">
      <star-outline />
    </button>
</template>



  </section>
</template>

<script>
  import starOutline from "vue-material-design-icons/StarOutline.vue"
  import star from "vue-material-design-icons/Star.vue"

  export default {
    name: 'chuckNorrisJokes',
    props: {
      joke: null,
      id: null
    },
    components: {
      star,
      starOutline
    },
    methods: {
      toggleFavorite: function(val, i){
        this.$emit('toggleFavorite', val, i);
      }
    }
  }
</script>

<style scoped lang="less">

button{
  background: transparent;
  border: none;
  font-size: 22px;
  padding: 0;
  color: #e67e22;
  cursor: pointer;
  position: relative;
  &:before{
    content: '';
    width: 0;
    height: 0;
    background: fade(#e67e22, 8%);
    display: block;
    border-radius: 50%;
    top: 50%;
    left: 50%;
    position: absolute;
    transform: translate(-50%, -50%);
    transition: height .2s, width .2s;
    }
    &:hover:before{
        width: 45px;
        height: 45px;

    }
    &:active:before{
      width: 25px;
      height: 25px;
    }
}

</style>
