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
        <div id="login-button" :style="{'background-color': checkState()}" @click="changeState(), updateCookies()">Login
            <div id="login-separator"></div>
            <span class="material-symbols-outlined" style="color:white;" v-if="logState=='login'">login</span>
            <span class="material-symbols-outlined" style="color:white;" v-else-if="logState=='success'">done</span>
            <span class="material-symbols-outlined" style="color:white;" v-else-if="logState=='logout'">logout</span>
            <span class="material-symbols-outlined" style="color:white;" v-else-if="logState=='error'">error</span>
            <img id="loading-svg" src="../assets/svg/ring-resize.svg" alt="loading-svg" v-else-if="logState=='loading'"/>
        </div>
     </main>
 </template>

 <script>
    import sleep from '../assets/util'

    export default {
        data() {
            return {
                user: '',
                id: '',
                grade: '',
                logState: 'login'
            }
        },

        created() {
            this.checkState()

            if (document.cookie == "") return
            var cookies = document.cookie
                .split(';')
                .map(cookie => cookie.split('='))
                .reduce((accumulator, [key, value]) => ({ ...accumulator, [key.trim()]: decodeURIComponent(value) }), {});
            this.$data.user = cookies['user']
            this.$data.id = cookies['id']
            this.$data.grade = cookies['grade']
        },

        methods: {
            async changeState() {
                this.$data.logState = 'loading'
                await sleep(3000) // SIMULATING LOAD TIME, DELETE LATER
                this.$data.logState = 'success'
                await sleep(2000)
                this.$data.logState = 'logout'
            },

            checkState() {
                if (this.$data.logState == 'login') 
                    return getComputedStyle(document.documentElement).getPropertyValue('--primary')
                else if (this.$data.logState == 'success') 
                    return getComputedStyle(document.documentElement).getPropertyValue('--success')
                else if (this.$data.logState == 'logout') 
                    return getComputedStyle(document.documentElement).getPropertyValue('--logout')
                else if (this.$data.logState == 'error') 
                    return getComputedStyle(document.documentElement).getPropertyValue('--error')
                else if (this.$data.logState == 'loading') 
                    return getComputedStyle(document.documentElement).getPropertyValue('--primary-lite')
            },

            updateCookies() {
                document.cookie = 'user=' + this.user + ';Secure;SameSite=Strict;'
                document.cookie = 'id=' + this.id + ';Secure;SameSite=Strict;'
                document.cookie = 'grade=' + this.grade + ';Secure;SameSite=Strict;'
            }
        }

    }
 </script>

 <style lang="scss">
    body {
        background-color: var(--primary-dark);
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

        &:focus {
            outline: 0.15rem solid var(--primary);
        }
    }

    #login-button {
        cursor: pointer;
        border-radius: 0.5rem;
        width: fit-content;
        padding: 0.5rem 0.75rem 0.5rem 0.75rem;
        color: var(--light);
        background-color: var(--success);
        display: flex;
        justify-content: center;
        align-items: center;

        transition: opacity 0.2s;
        opacity: 100%;

        &:hover {
            transition: opacity 0.2s;
            opacity: 80%;
        }

        #login-separator {
            margin-right: 0.5rem;
            margin-left: 0.5rem;
            width: 0.1rem;
            background-color: white; 
            height: 1.5rem;
            opacity: 60%;
        }
    }

    #loader-svg {
        filter: invert(1);
    }
 </style>