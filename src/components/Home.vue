<template>
    <h1>Hello USer</h1>
</template>
<script>
    export default {
        name:'Home',
        mounted()
        {
            let user =localStorage.getItem('user');
            if(!user){
                this.$router.push({name:'Signup'})
            }
        }
    }
</script>