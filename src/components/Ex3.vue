<script>
// Import BlogPost component
import blogPost from './subcomponents/BlogPost2.vue'
import axios from 'axios'
export default {
    data() {
        return {
            posts: [] // array of post objects
        }
    },
    computed: {
        baseUrl() {
            if (window.location.hostname == 'localhost' || window.location.hostname == '127.0.0.1')
                return 'http://localhost:3000'
            else {
                const codespace_host = window.location.hostname.replace('5173', '3000')
                return `https://${codespace_host}`;
            }
        }
    },
    created() { // created is a hook that executes as soon as Vue instance is created
        axios.get(`${this.baseUrl}/posts`)
            .then(response => {
                // this gets the data, which is an array
                this.posts = response.data
                console.log(response.data)
            })
            .catch(error => {
                this.posts = [{ entry: 'There was an error: ' + error.message }]
            })
    },
    methods: {
        deletePost(id) {
            axios.get(`${this.baseUrl}/deletepost`, { params: { id: id }})
                .then(response => {
                    // this gets the data, which is an array
                    console.log(response.data);
                    axios.get(`${this.baseUrl}/posts`)
                        .then(response => {
                            // this gets the data, which is an array
                            this.posts = response.data
                        })
                        .catch(error => {
                            this.posts = [{ entry: 'There was an error: ' + error.message }]
                        })
                })
                .catch(error => {
                    this.posts = [{ entry: 'There was an error: ' + error.message }]
                })
        }
    },
    components: {
        blogPost
    }
}
</script>

<template>
    <!-- TODO: make use of the 'blog-post' component to display the blog posts -->
    <blogPost v-for="post in posts" v-bind:entry="post.entry" v-bind:subject="post.subject" v-bind:mood="post.mood">
        <template v-slot:delete>
            <button @click="deletePost(post.id)">Delete</button>
        </template>
    </blogPost>
</template>
