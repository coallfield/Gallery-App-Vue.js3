<template>
    <div class="description">
        <div class="background">
            <div class="background-image">
                <img class="back-img" :src="photo.urls.full">
            </div>
        </div>
        
        <div class="main-image"> 
            <div class="image-description">
                <div class="description-text">
                    <h4>{{ photo.alt_description }}</h4>
                </div>
                <div class="btns-wrapper">
                    <button @click="addToFavourite(photo)"><img class="fav" src="@/img/make-favourite.png"></button>
                    <a :href="`data:${photo.urls.full}`" download="image.jpg"><button><img class="download" src="@/img/downloand.png"></button></a>
                    <a :href="`data:${photo.urls.full}`" download><button><img class="download-small" src="@/img/small-download.png"></button></a>
                </div>
            </div>   
            <div class="current-image">
                <img class="main-current-img" :src="photo.urls.regular">
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        photo: {
            type: Object,
            required: true
        }
    },
    methods: {
        addToFavourite(photo) {
            this.$emit('addToFavourite', photo)
           
        }, 
    }

}
</script>

<style scoped>

.main-image {
    
    position: absolute;
    width: 100%;
    display: flex;
    justify-content: center;
    top: 40%;
    
}

.download-small {
    display: none;
}
.main-current-img{ 
    max-width: 1100px;
    max-height: 1100px;
    box-shadow: 10px 5px 5px black;;
}

.background {
    background-color: rgb(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    overflow: hidden;
    max-height: 500px;
  
}

.btns-wrapper {
    display: flex;
    flex-direction: row;
}



.background-image{
    background-color:black;
    filter: grayscale(100%) blur(2px);
}  
.back-img {
    opacity: 50%;
    
}
 
.image-description {
   position: absolute;
   bottom: 105%;
    display: flex;
    gap: 500px;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;

}

.description-text {
  
    color: white;
    width: 300px;
    word-break: break-all;
    word-wrap: break-word;
}

</style>