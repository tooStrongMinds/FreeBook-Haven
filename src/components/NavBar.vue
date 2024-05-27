<template>
    <div class="container">
        <router-link to="/" class="nav-link"><i class="fa-solid fa-house fa-xl"></i>Home</router-link>
        <router-link to="/explore" class="nav-link"><i class="fa-regular fa-compass"></i>Explore</router-link>
        <router-link to="/library" class="nav-link"><i class="fa-solid fa-book-bookmark fa-xl"></i>Library</router-link>
    </div>
</template>

<script>
export default {

}
</script>

<style scoped>
.container {
    display: flex;
    gap: 30px;
}
.nav-link {
    display: flex;
    align-items: center;
    gap: 5px;
}
.nav-link:not(i) {
    font-size: 20px;
}
i {
    color: #e16a00;
    font-size: 20px;
}

</style>