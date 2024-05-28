<template>
    <div class="menu">
        <div class="icon">
            <i class="fas fa-bars"
            @click="showMenu()" v-if="!showMobileMenu">
            </i>
        </div>
        <div class="menuContent" :class="this.showMobileMenu ? 'open-menu' : 'close-menu'">
            <i class="fa-solid fa-xmark" @click="closeMenu()" v-if="showMobileMenu"></i>
            <div class="navigation" :class="!showMobileMenu ? 'none' : 'show'" @click="closeMenu">
                <router-link to="/" class="nav-link"><i class="fa-solid fa-house fa-xl"></i>Home</router-link>
                <router-link to="/explore" class="nav-link"><i class="fa-regular fa-compass"></i>Explore</router-link>
                <router-link to="/library" class="nav-link"><i class="fa-solid fa-book-bookmark fa-xl"></i>Library</router-link>
            </div>
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
    .menuContent {
       display: flex;
       flex-direction: column;
       gap: 20px;
    }
    .fa-xmark {
        font-size: 25px;
        text-align: left;
        padding-left: 20px;
    }
    .navigation {
        display: flex;
        flex-direction: column;
        gap: 30px;
        padding-left: 20px;
        
    }
    .none {
        display: none;
    }
    .show {
        display: flex;
        gap: 30px;
    }
    .open-menu {
        background: #241400;
        padding-top: 30px;

        position: absolute;
        top: 0;
        left: 0;
        padding-right: 100vw;

        transform: translateY(0%);
        transition: all 0.5s ease-in-out;
        height: 100vh;
        
    }
    .close-menu {
    
        height: 0;
        padding: 0;
        transform: translateY(0%);
        transition: all 0.5s ease-in-out;
    
    }
}

</style>