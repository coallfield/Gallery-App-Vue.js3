<template>
    <div class="header">
        <div class="header-main">
          <div class="input-wrap">
              <input @input="getSearchPhotos($event.target)" :value=findPhoto class="input" type="text" placeholder="Поиск">
          </div>
          <div class="background-image">
            <img class="background" src="@/img/background.png">
          </div>
        </div>
    </div>
</template>

<script>


export default {
  data() {
    return {
      urlSearch: 'https://api.unsplash.com/search/photos?query=renaissance&per_page=100&client_id=XG0LNq0HOjBurUYhK7WH8hwtelL8JadP1fM2feLSfP4&orientation=squarish&collections=58069144',
      photosFromSearch: {}
    }
  },
  props: {
    showButton: {
      type: Boolean
    },
    findPhoto: {
        type: String
    }
  },
  methods: {
    hideDesciption(bool) {
      this.$emit('hideDescription', bool)
    },
    async searchPhotos() {
      const respone = await fetch(this.urlSearch)
      this.photosFromSearch = await respone.json()
    
    },
    getSearchPhotos(event){
        this.$emit('update:findPhoto', event.value)
        this.$emit('searchPhotos', this.photosFromSearch.results)
    }
  },
  mounted() {
    this.searchPhotos()
  }

}
</script>

<style scoped>


.background-image {
  background-color: black;
  height: 253px;
}

.background {
  opacity: 50%;
}

.input-wrap {
  position: relative;
}

.input {
  font-size: 1rem;
  font-weight: bold;
  padding-left: 20px;
  position: absolute;
  margin-top: 90px;
  left:25%;
  z-index: 999;
  border: none;
  width:866px;
  height: 70px;
  outline: none;
  background: url('@/img/search.png') no-repeat white;
  background-position: right 20px bottom 23px;
}

</style>