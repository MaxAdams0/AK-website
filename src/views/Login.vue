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
         <button id="signin-button">Sign In</button>
         <img id="loading-svg" src="../assets/svg/ring-resize.svg" alt="loading-svg"/>
     </main>
 </template>

 <script>

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

    #signin-button {
        margin-top: 1.0rem;
        padding: 0.5rem 0.75rem 0.5rem 0.75rem;
        border-radius: 0.25rem;
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
 </style>