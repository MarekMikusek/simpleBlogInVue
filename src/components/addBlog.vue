<template>
    <div id="add-blog">
        <h1>Add new Blog Post</h1>
        <form>
            <label for="title-input">Blog title</label>
            <input type="text" id="title-input" v-model.lazy="blog.title">
            <label for="content-input">Blog content</label>
            <input type="text" id="content-input" v-model.lazy="blog.content">
            <div id="checkboxes">
                <label>Ninjas</label>
                <input type="checkbox" id="input-ninjas" v-model="blog.categories" value="ninjas">
                <label for="input-wizards">Wizards</label>
                <input type="checkbox" id="input-wizards" v-model="blog.categories" value="wizards">
                <label for="input-mario">Mario</label>
                <input type="checkbox" id="input-mario" v-model="blog.categories" value="mario">
                <label for="input-cheese">Cheese</label>
                <input type="checkbox" id="input-cheese" v-model="blog.categories" value="cheese" >
            </div>
            <select v-model="blog.author">
                <option v-for="author in authors">{{author}}</option>
            </select>
            <button @click.prevent="post">Save blog</button>
        </form>
        <hr />
        <div id="preview">
            <h3>Preview blog</h3>
            <p>Blog title: {{blog.title }}</p>
            <p>Blog content:</p>
            <p>{{ blog.content}}</p>
            <p>Blog categories:</p>
            <ul>
                <li v-for="category in blog.categories">{{ category }}</li>
            </ul>
            <p>Auhor: {{ blog.author }}</p>
        </div>
    </div>
</template>

<script>
    import searchMixin from '../mixins/searchMixin'
    export default {
        name: 'app',
        data() {
            return {
                blog: {
                    title: '',
                    content: '',
                    categories: [],
                    author: ''
                },
                authors: ['The Net Ninja', 'The Angular Avenger', 'Vue Master'],
                submitted: false
            }
        },
        methods: {
            post: function () {
                this.$http.post('https://vue-blog-list-marek.firebaseio.com/posts.json', this.blog).then(function (data) {
//                    console.log(data);
                });
            }
        },
        created() {
        },
        computed: {
        },
        filters: {},
        directives: {
        }
    }

</script>

<style>
    body{
        margin: 0;
        font-family:'Nunito SemiBold';
    }
    #add-blog *{
        box-sizing: border-box;
    }
    #add-blog{
        margin: 20px auto;
        max-width: 500px;
    }
    label{
        display: block;
        margin: 20px 0 10px;
    }
    input[type="text"], textarea{
        display: block;
        width: 100%;
    }
    #preview{
        padding: 10px 20px;
        border: 1px solid #ccc;
        margin: 30px 0;
    }
    h3{
        margin-top: 10px;
    }
    #checkboxes input{
        display: inline-block;
        margin-right: 10px;
    }
    #checkboxes label{
        display: inline-block;
    }
</style>

