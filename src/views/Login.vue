<template>
    <main class="login-page">
         <h1>Login</h1>
         <span class="input-title">First And Last Name:</span>
         <input class="text-input" v-model="user" type="text"/>
         <br/>
         <span class="input-title">ID Number:</span>
         <input class="text-input" v-model="id" type="text"/>
         <br/>
         <span class="input-title">Grade:</span>
         <input class="text-input" v-model="grade" type="text"/>
         <br/>
         <div class="container" style="margin-top: 1.0rem;" @click="changeState()">
            <button id="signin-button">Sign In</button>
            <state-box component-type="state-box">
                <span class="material-symbols-outlined" style="color:white;" v-if="loginState=='success'">done</span>
                <span class="material-symbols-outlined" style="color:white;" v-if="loginState=='login'">login</span>
                <span class="material-symbols-outlined" style="color:white;" v-if="loginState=='logout'">logout</span>
                <span class="material-symbols-outlined" style="color:white;" v-if="loginState=='error'">error</span>
                <img id="loading-svg" src="../assets/svg/ring-resize.svg" alt="loading-svg" v-if="loginState=='loading'"/>
            </state-box>
         </div>
     </main>
 </template>

 <script>
    export default {
        data() {
            return {
                user: '',
                id: '',
                grade: '',
                loginState: 'login'
            }
        },

        methods: {
            changeState() {
                this.$data.loginState = 'logout'
            }
        }

    }
 </script>

 <style lang="scss">
    body {
        background-color: var(--primary-alt);
    }

    h1 {
        color: var(--light);
        margin-bottom: 1.0rem;
    }

    .input-title {
        color: var(--light);
        margin-right: 1.0rem;
    }

    .text-input {
        border: none;
        border-radius: 6px;
        padding: 0.3rem 0.5rem 0.3rem 0.5rem;
        width: 20.0rem;
        color: var(--light);
        background-color: var(--dark-alt);
        margin-bottom: 0.5rem;
    } .text-input:focus {
        outline: 0.15rem solid var(--primary);
    }

    .container {
        cursor: pointer;
        width: fit-content;
        border-radius: 0.5rem;
        overflow: hidden;
        display: flex;
    }

    #signin-button {
        padding: 0.5rem 0.75rem 0.5rem 0.75rem;
        background-color: var(--light);
        transition: all 0.2s;
        opacity: 100%;
    } #signin-button:hover {
        transition: all 0.2s;
        opacity: 80%;
    }

    #loader-svg {
        filter: invert(1);
    }

    #state-box {
        background-color: var(--success);
        width: 2.0rem;
        height: 2.0rem;
        display: flex;
        justify-content: center;
        align-items: center;
    }
 </style>