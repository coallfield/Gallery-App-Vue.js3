<template>
    <div class="header-items">
            <div class="logo-wrap">
                <img @click="toMain" src="@/img/logo.png" class="logo">
            </div>
            <div class="search-favourite-wrapper">
                <button @click="toMain" class="search-btn" v-if="showButton || showFavourite"><img src="@/img/search-head.png" class="search"></button>
                <button @click="toMain" class="small-search" v-if="showButton || showFavourite"><img src="@/img/search-small.png" class="search"></button>
                <button @click="this.$emit('update:showFavourite', true)" class="favourite-btn"><img src="@/img/favourite.png" class="favourite"></button>
                <button @click="this.$emit('update:showFavourite', true)" class="favourite-small"><img src="@/img/fav-small.png" class="favourite"></button>
            </div>
        </div>
</template>

<script>
export default {
    props: {
        showButton: {
            type: Boolean
        },
        showFavourite: {
            type: Boolean
        }
    },
    methods: {
        toMain() {
            this.$emit('update:showButton', false)
            this.$emit('update:showFavourite', false)
        }
    }
}
</script>

<style scoped>
.header-items {
  background-color: black;
  width: 100%;
  height: 140px;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
}

.search-favourite-wrapper {
    display: flex;
    flex-direction: row;
    gap: 20px;
    align-items: center
  
}


.search-btn {
   
    display: flex;
    background: none;
    outline: none;
    border: none;
    align-self: center;
    
}

.favourite-btn {
    background: none;
    outline: none;
    border: none;

}

.small-search{
    display: none;
    background: none;
    outline: none;
    border: none;
}
.favourite-small {
    display: none;
    background: none;
    outline: none;
    border: none;
}
</style>