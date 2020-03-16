<template>
       <div>
            <el-card class="box-card">
                <div slot="header" class="clearfix">
                    <h1 class="post-title"> {{post.title }}</h1>
                    <el-button  style="float: right; padding: 3px 0" type="text" @click="editPost(post.id)">View post</el-button>
                    <el-button  style="float: right; padding: 3px 0" type="text" @click="deletePost(post.id)">View post</el-button>
                </div>
                <div v-for="o in 4" :key="o" class="text item">
                  {{post.description}}
                </div>
            </el-card>
        </div>
</template>

<script>
    import { mapState } from 'vuex'
    export default {
        name: 'PostDetail',
        async fetch({ store, params, error, $axios }){
            const { data } = await $axios.get(`/posts/${params.id}`)
            store.dispatch('setPost', data)
        },
        computed: {
            ...mapState({
                post: state => state.post.singlePost
            })
        }
    }
</script>

<style lang="scss" scoped>

    
</style>