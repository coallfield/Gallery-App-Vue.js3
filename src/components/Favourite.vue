<template>
   
    <div class="favourite-window">
        <div class="favourite-content">
            <h1 class="title"> Избранное </h1>
            <h2 v-if="favouritePhotos.length === 0" class="nothing">Вы ничего не добавили</h2>
            <div class="gallery-wrapper">
                <div v-for="photo in favouritePhotos" class="img-wrap" :key="photo.id">
                    <button @click="deleteFromFav(photo)" class="delete">×</button>
                    <img @click="getImage(photo)" class="image" :src="photo.urls.small">
                </div>
            </div>
            <div class="top-btn-wrapper">
                <button @click="scrollToTop" class="top-btn"><img src="@/img/button_top.png"></button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        favouritePhotos: {
            type: Array,
            required: true
        }
    },
    methods: {
        scrollToTop() {
            window.scrollTo({ left: 0, top: 0, behavior: 'smooth' })
        },
        deleteFromFav(photo) {
            this.$emit('deleteFromFav', photo)
        }
    }
}
</script>

<style scoped>

.gallery-wrapper {
  margin-left: auto;
  margin-right: auto;
  width: 1400px;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
}

.title {
    margin-top: 20px;
    text-align: center;
}

.nothing {
    text-align: center;
}

.img-wrap {
  max-width: 400px;
  max-height: 400px;
  margin: 20px;
  overflow: hidden;
  border-radius: 15px;
  position: relative;
  display: inline-block

}

.delete {
color: white;
font-size: 3rem;
position:absolute;
left:90%;
top: -5%
}

.top-btn {

  outline: none;
  background: none;
  background-color: none;
  border: none;
  width: 49px;
  height: 49px;
}

.top-btn-wrapper {
  position: fixed;
  left: 95%;
  top: 93%
}
</style>