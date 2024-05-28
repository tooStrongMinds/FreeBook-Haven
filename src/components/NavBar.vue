<template>
    <div :class="{'scrolled-nav': scrollPosition}">
        <div class="menuContent" :class="this.showMobileMenu ? 'open-menu' : 'close-menu'">
            <div class="navigation" @click="closeMenu">
                <router-link to="/" class="nav-link"><i class="fa-solid fa-house fa-xl"></i>Home</router-link>
                <router-link to="/explore" class="nav-link"><i class="fa-regular fa-compass"></i>Explore</router-link>
                <router-link to="/library" class="nav-link"><i class="fa-solid fa-book-bookmark fa-xl"></i>Library</router-link>
            </div>
        </div>
        <div class="icon">
            <i class="fas fa-bars"
            @click="showMenu()" v-if="!showMobileMenu">
            </i>
            <i class="fa-solid fa-xmark" @click="closeMenu()" v-if="showMobileMenu"></i>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            showMobileMenu: false
        }
    },
    methods: {
    showMenu() {
      this.showMobileMenu = true
    },
    closeMenu() {
      this.showMobileMenu = false
    },
    }
}
</script>

<style scoped>
.navigation {
    display: flex;
    gap: 20px;
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

@media (max-width: 760px) {
    .icon {
        display: unset;
    }
    .navigation {
        display: block;
    }
    .open-menu {
        opacity: 1;
        background: yellowgreen;
        padding-top: 20px;
    }
    .close-menu {
        opacity: 1;
        height: 0;
        padding: 0;
    }
}

</style>