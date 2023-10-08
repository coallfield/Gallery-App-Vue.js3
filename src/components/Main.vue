<template>
    <div class="main">
        <div class="gallery-wrapper">
            <div v-for="photo in photos" class="img-wrap" :key="photo.id">
                <img @click="getImage(photo)" class="image" :src="photo.urls.small">
            </div>
        </div>
        <div class="top-btn-wrapper">
            <button @click="scrollToTop" class="top-btn"><img src="@/img/button_top.png"></button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        photos: {
            type: Array,
            required: true
        },
        showDescription: {
          type: Boolean
        }
    },
    methods: {
        scrollToTop() {
            window.scrollTo({ left: 0, top: 0, behavior: 'smooth' })
        },
        getImage(id) {
          this.$emit('update:showDescription', true)
          this.$emit('getImage', id)
        }
    }

}
</script>

<style scoped>
.main {
  margin-top: 40px;
}

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
.image {
  max-width: 400px;
  max-height: 400px;
}

.img-wrap {
  max-width: 400px;
  max-height: 400px;
  margin: 20px;
  overflow: hidden;
  border-radius: 15px;
  

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