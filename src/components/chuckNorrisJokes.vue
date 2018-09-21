<template>
  <div id="jokes">

    <template v-if="!loaded">
      <div class="init-jokes">
        <h1>Get started by pressing the button below</h1>
        <button @click="getJokes" class="init-jokes_button"> Load Jokes </button>
      </div>
    </template>

    <template v-else-if="loaded">
      <header>
        <h1>Jokes</h1>
        <button @click="getJokes"> Get fresh Jokes!</button>
      </header>

      <section>
        <ul class="joke-list">
          <li v-for="(joke, index) in jokes" class="joke-list_item">
            <div class="list-container">

              <div class="joke-content">
                {{joke.joke}}
              </div>

              <div class="joke-actions">
                  <FavoriteIcon :joke="joke.joke" :id="joke.id" @toggleFavorite="toggleFavorite(joke.joke, joke.id, index)"/>
              </div>

            </div>
          </li>
        </ul>
      </section>

    </template>


  </div>
</template>

<script>
  import FavoriteIcon from '@/components/FavoriteIcon.vue'

  export default {
    name: 'chuckNorrisJokes',
    props: {
      jokes: {},
      loaded: false
    },
    components: {
      FavoriteIcon
    },
    methods: {
      getJokes: function(){
        this.$emit('getJokes');
      },
      toggleFavorite: function(val, i, index){
        this.$emit('toggleFavorite', i, val, index);
      }
    }
  }
</script>

<style scoped lang="less">
  #jokes{
    position: relative;
    background: fade(#000, 4%);
    .init-jokes{
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 75%;
      text-align: center;
      h1{
        font-size: 22px;
        font-weight: 400;
        letter-spacing: 0.075em;
        margin-bottom: 40px;
      }
    }
    .init-jokes_button, header button{
      border: solid 1px #1abc9c;
      color: #1abc9c;
      background: transparent;
      border-radius: 40px;
      padding: 10px 30px;
      cursor: pointer;
      transition: background .3s, color .3s;
      &:hover{
        color: #fff;
        background: #1abc9c;
      }
    }
    .joke-list{
      list-style: none;
      padding: 0;
      margin: 50px auto 0 auto;
      width: 90%;
      max-width: 750px;
      &_item{
        margin: 20px 0;
        background: #fff;
        box-shadow: 0 5px 10px fade(#000, 8%);
        border-left: solid 3px #1abc9c;
        .list-container{
          display: flex;
          flex-wrap: nowrap;
          .joke-content{
            padding: 20px;
            width: calc(~'100% - 100px');
            line-height: 25px;
          }
          .joke-actions{
            width: 100px;
            button{
              width: 100%;
              height: 100%;
            }
          }
        }
      }
    }
  }
</style>
