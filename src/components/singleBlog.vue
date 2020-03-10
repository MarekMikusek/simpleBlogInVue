<template>
    <div id="single-blog">
        <h1>Blog title: {{ blog.title }}</h1>
        <article>Blog content:  {{ blog.content }}</article>
        <p>Author: {{ blog.author }}</p>
        <p>Blog categories: </p>
        <ul>
            <li v-for="category in blog.categories">{{ category }}</li>
        </ul>
    </div>
</template>
<script>
    export default{
        data() {
            return{
                id: this.$route.params.id,
                blog: {
                    title: 'importing data',
                    body: ''
                }
            }
        },
        created() {
            this.$http.get('https://vue-blog-list-marek.firebaseio.com/posts/'+this.id+'.json').then(function(data){
                return data.json();
            }).then(function(data){
                this.blog = data;
            });
        }
    }
</script>
<style scoped>
    #single-blog{
        width: 70%;
        margin: 0 auto;
    }
</style>

