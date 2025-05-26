<template>
    <div class="one">
        <h1 class="elem">{{ product.title }}</h1>
        <h2 class="elem">price : {{ product.price }}</h2>
        <h3 class="elem">Brief description about this item : {{ product.description }}</h3>
        <h4 class="elem">Category : {{ product.category }}</h4>
        <img :src="product.image" :alt="product.id">
        <button @click="remove1">Remove this item</button>

    </div>
</template>
<script>
export default {
    data(){
        return {
            product : {}, 
        } 
    }, 
    mounted () {
        this.fetchproduct(); 
    },  
    methods :{
        async remove1(){
            const id=this.$route.params.id; 
            await fetch(`http://localhost:3000/data/${id}`,{method:'DELETE'}) 
            this.$router.push("/products");
            


        },
        async fetchproduct(){
            const id=this.$route.params.id; 
            const res= await fetch(`http://localhost:3000/data/${id}`);
            this.product= await res.json(); 
        }
    }
}
</script>

<style>
img {
    width:250px;
    margin-left:400px;
}
.prod{
    display:"flex"; 
    flex-direction: column ;

}
.one {
    display: "flex";
    flex-direction: "column";
    background-color: rgb(30, 95, 96);
    margin:20px; 
    border-radius:4px;
    padding:10px; 
    color : white; 
}
.elem {
    padding-left : 30px; 
    padding : 10px; 
}
input {
    width :100%; 
    height : 30px;
    margin : 10px; 
}
.det{
    margin-left: 100px; 
    width:160px; 
    height : 30px; 
    color :white; 
    font-size: larger;
    font-weight: bold;
}

</style>