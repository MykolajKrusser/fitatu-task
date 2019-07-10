<template>
    <div class="app">
        <Header />
        <div class="pages-container">
            <router-view />
        </div>
        <Footer />
    </div>
</template>
<script>
    import Header from '@components/Header';
    import Footer from '@components/Footer';

    export default {
        components: {
            Header,
            Footer,
        }
    };
</script>
<style lang="scss" scoped>
    
    .app {
        min-height: 100vh;
        min-width: 100vw;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }

    .pages-container {
        max-width: 1080px;
        margin: 0 auto;
    }
</style>