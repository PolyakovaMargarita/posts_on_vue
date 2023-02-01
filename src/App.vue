<template>
    <div class="app">
        <div class="container" >
            <h1 style="margin-bottom: 25px">Posts page</h1>
            <div class="app_btns">
                <my-button @click="showDialog">Add post</my-button>
                <my-select></my-select>
            </div>
            <my-dialog :show="dialogVisible" @update:show="dialogVisible = $event">
                <post-form
                @create="createPost"
            />
            </my-dialog>
            <post-list
                style="margin-top: 15px"
                :posts="posts"    
                @remove="removePost" 
                v-if="!isPostLoading"
            />
            <div v-else>Loading...</div>
        </div>
    </div>
</template>

<script>
import PostList from "@/components/PostList.vue"
import PostForm from "@/components/PostForm.vue"
import axios from "axios"

    export default {
        components: {
            PostForm, PostList
        },
        data() {
            return {
                posts: [],
                dialogVisible: false,
                isPostLoading: false
            }
        },
        methods: {
            createPost(post) {
                this.posts.push(post)
                this.dialogVisible = false
            },
            removePost(post) {
                this.posts = this.posts.filter((p) => p.id !== post.id)
            },
            showDialog() {
                this.dialogVisible = true
            },
            async fetchPosts() {
                try {
                    this.isPostLoading = true
                    const response = await axios.get(`https://jsonplaceholder.typicode.com/posts?_limit=10`)
                    this.posts = response.data
                } catch(e) {
                    console.log(e)
                    alert("error")
                } finally {
                    this.isPostLoading = false
                }
            },
        },
        mounted() {
                this.fetchPosts()
        }   
    }

</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
.app {
    display: flex;
    justify-content: center;
    margin-top: 20px;
    max-width: 1980px;
}
.container {
    width: 95%;
}
.app_btns {
    display: flex;
    justify-content: space-between;
}
</style>