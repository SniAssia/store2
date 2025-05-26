<template>
    <form>
        <input v-model="title" placeholder="enter the name of the product">
        <input v-model="price" placeholder="enter the price">
        <input v-model="description" placeholder="enter the description">
        <input v-model="category" placeholder="enter the category">
        <button @click.prevent="addnewproduct">submit</button>
    </form>

</template>
<script>
export default {
    data(){
        return {
             title:"", 
             price:"", 
             description:"", 
             category :"", 
        }
    }, 
    mounted(){

    }, 
    methods : {
        async addnewproduct(){
            
            const product = {"title" : this.title, 
                            "price" : this.price, 
                            "description" : this.description, 
                            "category" : this.category, 
        }; 
            const ref = await fetch('http://localhost:3000/data', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(product)
                }); 
            alert("object added successefully"); 
            this.title="";
            this.price="";
            this.description=""; 
            this.category="";
        }
    }
}
</script>