<template>
    <div v-theme:column="'narrow'" id="show-blogs">
        <h1>All blog articles</h1>
        <input v-model="search" type="text" placeholder="search posts">
        <div v-for="blog in filteredBlogs" class="single-blog">
            <router-link v-bind:to="'/blog/'+blog.id"><h2 v-rainbow>{{blog.title | to-uppercase  }}</h2></router-link>
            <article v-largerFont>{{ blog.content }}</article>
        </div>
    </div>
</template>

<script>
    import searchMixin from '../mixins/searchMixin'
    export default {
        name: 'app',
        data() {
            return {
               blogs: [],
               search:''
            }
        },
        created(){
            this.$http.get('https://vue-blog-list-marek.firebaseio.com/posts.json')
                    .then(function(data){
                       return data.json();
//                        this.blogs = data.body;
            }).then(function(data){
                let blogsArray=[];
                for (let key in data){
                    data[key]['id'] = key;
                    blogsArray.push(data[key]);
                }
                this.blogs = blogsArray;
            });
        },
        computed:{
      
        },
        filters:{
      
        },
        directives:{
            'largerFont':{
                bind(el, binding, vnode){
                    el.style.fontSize = '2em';
                }
            }
        },
        mixins:[searchMixin]
                
    }
</script>

<style>
    #show-blogs{
        max-width: 800px;
        margin: 0 auto;
    }
    .single-blog{
        padding: 20px;
        margin: 20px 0;
        box-sizing: border-box;
        background-color: #eee;
    }
</style>
