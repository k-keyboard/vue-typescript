<template>
    <div>
        <h1>{{title}}</h1>
        <form>
            <label for="username">username : </label>
            <input type="text" name="username" id="username" v-model="states.account.user">
            <br>
            <label for="password">password : </label>
            <input type="password" name="password" id="password" v-model="states.account.pass">
            <br>
            <button @click="onClickLogin">Submit</button>
            <button type="button" @click="onClickClear">Reset</button>
            <br>
            <span>#Debug: {{states.account}}</span>

        </form>
    </div>
</template>
<script lang="ts">
import { defineComponent,  reactive } from 'vue'
import User from '../types/user.type'

interface LoginState{
    account: User
}
export default defineComponent({
    emits:["submitLogin"],
    props:["title"],
    setup(props, {emit}) {
        const states = reactive<LoginState>({account: {user:"",pass:""}})

        const onClickClear =()=>{
            states.account = {user:"",pass:""}
        }
        const onClickLogin =()=>{
            emit("submitLogin", states.account)
        }
        {
            return{
                states,
                onClickClear,
                onClickLogin
            };
        }
    },
})
</script>
