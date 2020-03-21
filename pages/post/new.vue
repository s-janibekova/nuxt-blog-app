<template>
    <div class="mainContent">
        <h3 class="title">New post</h3>
        <el-form ref="form" :model="form" :rules="rules" label-width="120px" text-align="center">
            <el-form-item label="Title" prop="title">
                <el-input v-model="form.title"></el-input>
            </el-form-item>
             <el-form-item label="Descritpion" prop="description">
                <el-input type="textarea" v-model="form.description"></el-input>
            </el-form-item>
            <el-form-item>
                <el-button  type="primary" @click="onSubmit('form')">Create</el-button>
                <el-button ref="button" @click="resetForm('form','button')">Cancel</el-button>
            </el-form-item>
        </el-form>
    </div>
</template>

<script>
    export default {
        name: 'PostList',
        data(){
            return {
                form : {
                title: '',
                description: ''
                },
                rules : {
                  title: { required: true, message: 'Please input activiry name', trigger: 'blur' } ,
                  description: { required: true, message: 'Please provide the post description', trigger: 'blur' } 
                }
            }
        },
        methods: {
            onSubmit(form) {
                this.$refs[form].validate((valid) => {
                    if(valid) {
                        alert("Form is submitted")     
                        this.$store.dispatch('savePost', {
                        id: Date.now().toString(),
                        title: this.form.title,
                        description: this.form.description
                    })
                    this.$router.push({path: '/post/list'})    

                    } else {
                        console.log("error submit!")
                        return false 
                    }
                }) 
            },
                resetForm(form, button) {
                    this.$refs[form].resetFields(this.title);
                    console.log(this.$refs[form])
            }  

        }

    }
</script>

<style>
 .title {
    text-align: center;
}
.mainContent {
    margin: 5rem 7rem;
}

</style>