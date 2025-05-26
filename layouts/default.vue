<template>
    <header>
    <div class="b">
        <div class="a">
            <NuxtLink to="/">
                <p>Home page</p>
            </NuxtLink>
        </div>
        <div  class="a">
            <NuxtLink to="products">
                <p>Products</p>
            </NuxtLink>
        </div>
        <div  class="a">
            <NuxtLink to="about">
                <p>About the store</p>
            </NuxtLink>
        </div>
        <div class="a">
            <NuxtLink to="addproject">
                <p>add product</p>
            </NuxtLink>
        </div>
    </div>
    </header>
    <div>
        <NuxtPage />
    </div>
</template>
<style>
.b {
    display: flex;
    flex-direction: row ; 
    justify-content: space-around;
    background-color: rgb(142, 155, 163);
    padding : 10px;
    color:white; 

    margin : 10px; 
}
.a{
    border-radius: 4px; 

}
</style>