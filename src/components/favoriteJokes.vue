<template>
  <div id="favorites">

    <header>
      <h1>Favorites</h1>
      <template v-if="favorites.length">
        <span>({{favorites.length}})</span>
      </template>
    </header>

    <section>

      <ul class="favorite-list">
        <li v-for="(fav, index) in favorites" class="favorite-list_item">
          <div class="list-container">

            <div class="favorite-content">
              {{fav.joke}}
            </div>

            <div class="favorite-actions">
              <button @click="deleteFavorite(fav.id, fav.val)"> <deleteOutline /> </button>
            </div>

          </div>
        </li>
      </ul>

    </section>

  </div>
</template>

<script>
  import deleteOutline from "vue-material-design-icons/DeleteOutline.vue"
  export default {
    name: 'favoriteJokes',
    props: {
      favorites: {}
    },
    components: {
      deleteOutline
    },
    methods: {
      deleteFavorite: function(id, val){
        this.$emit("deleteFavorite", id, val)
      }
    }
  }
</script>

<style scoped lang="less">
  #favorites{
    background: #1abc9c;
    header{
      h1{
        color: #fff;
      }
      span{
        color: #fff;
        font-size: 18px;
        letter-spacing: 0.075em;
      }
    }
    .favorite-list{
      list-style: none;
      padding: 0;
      margin: 50px auto 0 auto;
      width: 90%;
      max-width: 750px;
      &_item{
        margin: 20px 0;
        background: #fff;
        box-shadow: 0 5px 10px fade(#000, 8%);
        border-left: solid 3px darken(#1abc9c, 15%);
        .list-container{
          display: flex;
          flex-wrap: nowrap;
          .favorite-content{
            padding: 20px;
            width: calc(~'100% - 100px');
            line-height: 25px;
          }
          .favorite-actions{
            width: 100px;
            button{
              width: 100%;
              height: 100%;
              color: #e74c3c;
              background: transparent;
              border: none;
              padding: 0;
              font-size: 22px;
              position: relative;
              cursor: pointer;
              &:before{
                content: '';
                width: 0;
                height: 0;
                background: fade(#e74c3c, 8%);
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
          }
        }
      }
    }
  }
</style>
