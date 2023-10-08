<template>
  <div class="app">
    
    <HeadInfo v-model:showFavourite="showFavourite" v-model:showButton="showDescription"></HeadInfo>
    <div v-if="showFavourite" class="hr"></div>
    <Favourite @deleteFromFav="deleteFromFav" :favouritePhotos="favouritePhotos" v-if="showFavourite"></Favourite>
    <Description @addToFavourite="addToFavourite" :photo="currentPhoto"  v-if="showDescription && !showFavourite"></Description>
    <Head @searchPhotos="searchPhotos" v-model:findPhoto="findPhoto" v-if="!showDescription && !showFavourite"></Head>
    <div v-if="!showDescription && !showFavourite" class="hr"></div>
    <Main @getImage="getImage" v-model:showDescription="showDescription" v-if="!showDescription && !showFavourite" :photos="findPhotos"></Main>
    
  </div>
  
  
</template>

<script>
import Head from '@/components/Head.vue'
import HeadInfo from '@/components/HeadInfo.vue'
import Main from '@/components/Main.vue'
import Favourite from '@/components/Favourite.vue'
import Description from '@/components/Description.vue'
export default{ 
  data() {
    return {
        urlRandom: `https://api.unsplash.com/photos/random?client_id=XG0LNq0HOjBurUYhK7WH8hwtelL8JadP1fM2feLSfP4&count=9&orientation=squarish&collections=58069144`,
        photos: [],
        currentPhoto: {},
        showFavourite: false,
        showDescription: false,
        favouritePhotos: JSON.parse(localStorage.getItem('photos')) || [],
        findPhoto: ''
       
    }
  },
  methods: {
    async fetchPhotos(url) {
        const response = await fetch(url)
        this.photos = await response.json()
    },
    getImage(photo) {
        this.currentPhoto = {...photo}
    },
    addToFavourite(photo) {
          this.favouritePhotos = this.favouritePhotos.filter(el => el.id !== photo.id)
          this.favouritePhotos.push(photo)
          localStorage.setItem('photos', JSON.stringify(this.favouritePhotos))
    },
    deleteFromFav(photo) {
      this.favouritePhotos = this.favouritePhotos.filter(el => el !== photo)
      localStorage.setItem('photos', JSON.stringify(this.favouritePhotos))
    },
    searchPhotos(photosSearch) {
        this.photos = photosSearch
        console.log(this.photos)
    }
  },
  mounted() {
      this.fetchPhotos(this.urlRandom)
      
  },
  computed: {
      findPhotos() {
        console.log(this.photos)
        return this.photos.filter(el => el.alt_description.toLowerCase().trim().includes(this.findPhoto.toLocaleLowerCase().trim()))
        
      }
  },    
  components: { Head, Main, Description, HeadInfo, Favourite }
}
</script>

<style>
* {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
 
  margin: 0;
  padding: 0;
  box-sizing: border-box;

}

@media(max-width: 1340px) {
  input.input {
    max-width: 700px;
  }
  div.gallery-wrapper {
    max-width: 1000px;
  }

}

@media(max-width: 1194px) {
   input.input {
    max-width:550px;
  }
  div.top-btn-wrapper {
    margin-left: -50px;
  }
  .search-btn[data-v-5a310cbe]{
    right: 33%;
  }
  div.image-description[data-v-7b5c0861] {
    position: absolute;
    bottom: 105%;
    display: flex;
    gap: 0px;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
  }
  img.main-current-img {
      width: 500px;
      height: 500px;
  }
}


@media(max-width: 638px) {
  .search-btn[data-v-5a310cbe]{
    right: 35%;
  }
  .description-text[data-v-7b5c0861] {
    width: 150px;
  }
  div.image-description[data-v-7b5c0861] {
    bottom: 102%;
    gap: 30px
  }
  .btns-wrapper[data-v-7b5c0861] {
    flex-direction: column;
    
  }
  .search-favourite-wrapper[data-v-5a310cbe] {
    flex-direction: column;
  }
}



@media(max-width: 964px) {
   input.input {
    max-width:350px;
    margin-left: 30px;
  }
  div.input-wrap {
    max-width: 906px;
  }
  div.gallery-wrapper {
    max-width: 700px;
  }
}

@media(max-width: 780px) {
   input.input {
   
    margin-left: 20px;
  }
  
}

@media(max-width: 680px) {
   input.input {
   
    margin-left: 10px;
  }
  
}






@media(max-width: 590px) {
   input.input {
    margin-left: -20px;
  }
  div.gallery-wrapper {
    max-width: 500px;
  }
  img.main-current-img {
      width: 300px;
      height: 300px;
  }
  .fav {
      width: 50px;
      height: 50px;
  }
  .download {
    display: none;
  }
  .download-small[data-v-7b5c0861]{
    display: block;
  }
  .btns-wrapper[data-v-7b5c0861] {
    flex-direction: row;
    
  }
}

@media(max-width: 462px) {
   input.input {
    margin-left: -17px;
    max-width: 250px;
  }
  
  img.image {
    width: 300px;
    height: 300px;
  }
  div.gallery-wrapper {
    max-width: 400px;
  }
}


.app {
 overflow-x: hidden;
}

.hr {
  width: 100%;
  height: 10px;
  background-color: grey;
}

button {
  background: none;
    outline: none;
    border: none;
}

</style>