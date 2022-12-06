<template>
    <div>
        <h1>App.Vue</h1>
        <span>#Debug1: {{count1}}</span> <br>
        <span>#Debug2: {{count2}}</span> <br>
        <button @click="onClickAdd1">Add1</button>
        <button @click="onClickAdd2">Add2</button>
        <hr>
        <span>#Account {{states.account}}</span> <br>
        <button @click="onClickClearAccount">Clear</button>
        <hr>
        <LoginForm title="Login" @submitLogin="onSubmitLogin" />
    </div>
</template>
<script lang="ts">
import { defineComponent, onMounted, reactive, ref } from 'vue'
import LoginForm from './components/LoginForm.vue'
import User from './types/user.type'

const defaultAccount = {user:"",pass:""}

export default defineComponent({
    components:{
        LoginForm
    },
    setup() {
        let count1 = 1;
        const count2 = ref<number>(2)
        const states = reactive({account:{
            user:"admin",
            pass:"1234"
        }})

        onMounted(() =>{
            // setInterval(onClickAdd2,1000)
        })
        const onClickAdd1 = ()=>{
            count1 = count1 + 1
            console.log("count1 = " + count1)
        }
        const onClickAdd2 = ()=>{
            count2.value = count2.value + 1
            console.log("count2 = " + count2.value)
        }
        const onClickClearAccount =()=>{
            // account.user=""
            // account.pass=""
            states.account = defaultAccount
        }
        const onSubmitLogin =(event:User)=>{
            alert(JSON.stringify(event))
        }
        return {
            count1,
            count2,
            onClickAdd1,
            onClickAdd2,
            states,
            onClickClearAccount,
            onSubmitLogin
        }
    },
})
</script>
