<template>
    <div>
        <app-header></app-header>
        <router-view></router-view>
    </div>
</template>

<script>
    import header from './components/Header.vue'
    import showBlogs from './components/showBlogs.vue'
    import listBlogs from './components/listBlogs.vue'
    import addBlog from './components/addBlog'
    import singleBlog from './components/singleBlog'
    
    export default {
        components: {
            'header': showBlogs,
            'show-blogs': showBlogs,
            'list-blogs': listBlogs,
            'app-header': header
        },
        name: 'app',
        data() {
            return {
            }
        }
    }
</script>

<style>

</style>
