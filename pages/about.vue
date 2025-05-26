<template>
        <div>
            <input v-model="my_id" placeholder="please enter your id here to get your personal cart ..(ex 1,2,3..)">
            <button @click="fetchproduct">Go to see my cart </button>
        </div>
     <div class="masquer" id="mine">
        <h1>You can find below your personal cart : </h1>
        <div v-for="cart1 in filtercarts" :key="cart1.id">
            <div>this cart was added since : {{ cart1.date }}</div>
            <ul>List of your products : </ul>
                <div v-for="product in products" :key="product.id">
                    <h1 class="elem">{{ product.title }}</h1>
                    <h2 class="elem">price : {{ product.price }}</h2>
                    <h3 class="elem">Brief description about this item : {{ product.description }}</h3>
                    <h4 class="elem">Category : {{ product.category }}</h4>
                    <img :src="product.image" :alt="product.id">

                </div>

            
        </div>
        <div>

        </div>
     </div>
</template>
<script>
export default {
    data(){
        return {
            carts:[],
            my_id: "", 
            products : [], 
            

        }
    }, 
    mounted(){
        this.fetchcarts();
        
    }, 
    methods :{
        async fetchcarts(){
            const resi=await fetch('https://fakestoreapi.com/carts'); 
            this.carts =await resi.json();
            
        }, 
        async fetchproduct(){
            this.products=[];
            for (const elem of this.filtercarts){
                for (const elem2 of elem.products){
                    const resi = await fetch(`https://fakestoreapi.com/products/${elem2.productId}`); 
                    this.products.push(await resi.json());
                }
            }
            document.getElementById("mine").style.display="block"; 
        },
    }, 
    computed : {
        filtercarts(){
            const my_id1=Number(this.my_id); 
            if (!this.my_id.trim()) return this.carts; 
            else {
                return this.carts.filter(elem =>
                elem.userId==my_id1
                )
            }
        },

    }, 
}
</script>
<style>
.masquer {
    display : none; 
}
</style>