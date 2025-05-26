<template>
    
    <div>
        <input v-model="elem" placeholder="rechercher par nom de l'article....">
    </div>
    <div class="prod" v-for="product in filterproduct" :key="product.id">
    <div class="one">
        <h1 class="elem">{{ product.title }}</h1>
        <h2 class="elem">price : {{ product.price }}</h2>
        <img :src="product.image" :alt="product.id">
        <NuxtLink :to="`products/${product.id}`">
            <p class="det">View Details</p>
        </NuxtLink>
    </div>
    </div>
</template>
<script>
export default {
    /*computed: {
  filterproducts() {
    const titleQuery = this.titleFilter?.trim().toLowerCase() || '';
    const categoryQuery = this.categoryFilter?.trim().toLowerCase() || '';

    return this.products.filter(product =>
      product.title.toLowerCase().includes(titleQuery) &&
      product.category.toLowerCase().includes(categoryQuery)
    );
  }
}
*/
    data() {
        return  {
            products : [], 
            elem: "", 
        }
    },
    computed : {

        filterproduct(){
            if (!this.elem.trim()) return this.products; 
            else {
                return this.products.filter(element=>
                element.title.toLowerCase().includes(this.elem.toLowerCase()) ||
                element.category.toLowerCase().includes(this.elem.toLowerCase())
                )
            }
        }
    }, 
    methods: {
        async fetchproducts(){
            const res = await fetch('http://localhost:3000/data'); 
            const data = await res.json(); 
            console.log(data)
            this.products=data; 
        },
    }, 
    mounted(){
        this.fetchproducts(); 
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
