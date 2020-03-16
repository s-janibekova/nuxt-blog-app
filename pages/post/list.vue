<template>
    <div>
            <el-card class="box-card"  v-for="post in posts" :key="post.id">
                <div slot="header" class="clearfix">
                    <h1 class="post-title"> {{post.title }}</h1>
                    <el-button  style="float: right; padding: 3px 0" type="text" @click="viewPost(post.id)">View post</el-button>
                </div>
                <div v-for="o in 4" :key="o" class="text item">
                  {{post.description.substr(0,70) }}
                </div>
            </el-card>
        </div>
</template>

<script>
import { mapState } from 'vuex'
    export default {
        name: 'PostList',
     
        async fetch({store, $axios, error}){
             try {
                const {data} = await $axios.get('/posts')
                store.dispatch('setPosts', data)
          
        } catch (err) {
          error({statusCode: 500, message: 'Ops, something went wrong'})
          }
        },
        
        computed: {
            ...mapState({
             posts: state => state.post.posts
            }),
        },
        methods: {
          viewPost(postId){
            this.$router.push({path:`/post/${postId}/detail` })
          }
        }
    }
</script>

<style>
  .post-title {
      text-align: center;
  }
  .text {
    font-size: 14px;
  }

  .item {
    text-align: center;
    margin-bottom: 18px;
    margin-left: 20px;
  }

  .clearfix:before,
  .clearfix:after {
    display: table;
    content: "";
  }
  .clearfix:after {
    clear: both
  }

  .box-card {
    width: 60%;
    margin: 20px auto 20px auto;
    padding: 20px;
  }
</style>