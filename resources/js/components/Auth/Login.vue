<template>
    <section class="auth-container">
        <h1>Login</h1>
        <form @submit.prevent="loginUser">
            <div class="form-group">
                <p v-for="error in errors" :key="error">
                    {{error}}
                </p>
                <label for="exampleInputEmail1">Email address</label>
                <input type="email" name="email" class="form-control" id="email"  placeholder="Enter email" v-model="form.email">
            </div>
            <div class="form-group">
                <label for="exampleInputPassword1">Password</label>
                <input type="password" name="password" class="form-control" id="exampleInputPassword1" placeholder="Password" v-model="form.password">
            </div>
            
            <input type="submit" value="Submit" class="btn btn-primary"/>
        </form>
    </section>
</template>

<script>
export default {
    data(){
        return{
            form:{
                email:'',
                password:'' 
            },
            errors:[]
        }
    },
    methods: {
        loginUser(){
            axios.post('/api/login',this.form).then(()=>{
                this.$router.push({name: 'Dashboard'});
            }).catch((error) => {
                this.errors = error.response.data.errors;
            })
        }
    }
}
</script>
