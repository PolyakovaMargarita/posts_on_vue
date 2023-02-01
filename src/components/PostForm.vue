<template>
    <form @submit.prevent>
        <h4>Add post</h4>
        <my-input 
            v-bind:value="post.title"
            @input="post.title = $event.target.value"
            placeholder="Name" />
        <!-- <my-input 
            v-modal:value="post.title"
            placeholder="Name" /> -->
        <my-input 
            v-bind:value="post.body"
            @input="post.body = $event.target.value"
            placeholder="Description" />
        <!-- <my-input 
            v-modal="post.body"
            placeholder="Description" /> -->
        <my-button class="btn" @click="createPost" style="align-self: flex-end; margin-top: 15px;">Add</my-button>
    </form>
</template>

<script>
    export default {
        data() {
            return {
                post: {
                    title: "",
                    body: "",
                }

            }
        },
        methods: {
            createPost() {
                this.post.id = Date.now()
                this.$emit("create", this.post)
                this.post = {
                    title: "",
                    body: "",
                }
            },
        }  
    }

</script>

<style scoped>
form {
    display: flex;
    flex-direction: column;
}
</style>