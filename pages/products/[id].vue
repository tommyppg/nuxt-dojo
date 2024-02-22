<template>
    <div>
        <Head>
            <Title>Nuxt Dojo | {{ product.title }}</Title>
            <Meta name="description" :content="product.description" />
        </Head>
        
        <ProductDetails :product="product"/>
    </div>
</template>

<script setup>
    definePageMeta({
        layout: 'products'
    }) //memilih layout mana yang akan dipilih

    const { id } = useRoute().params; //id sama dengan nama id
    const uri = 'https://fakestoreapi.com/products/' + id;

    const {data: product} = await useFetch(uri, { key: id});

    if(!product.value){
        throw createError({statusCode: 404, statusMessage: 'Product not found!', fatal: true}); //fungsi untuk melakukan 'redirect' jika error. fatal: untuk force jika terjadi error di halaman ini
    }
</script>

<style scoped>

</style>