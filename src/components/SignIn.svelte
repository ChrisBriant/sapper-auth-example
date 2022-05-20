<script context="module">
  // import {conn} from '../network/api';
  // const BASE_URL = 'http://localhost:8000';

  // export const authenticate2 = payload => {
  //     return new Promise(async (resolve,reject) => {
  //         try{
  //             const response = await conn.post('/api/account/authenticate/',payload);
  //             localStorage.setItem('access_token',response.data.access);
  //             localStorage.setItem('refresh_token',response.data.refresh);
  //             return resolve('Success');
  //         } catch(err) {
  //             console.log(err);
  //             if(err.response.data.message) {
  //               return reject(err.response.data.message);
  //             } else {
  //               return reject('An error occured trying to sign in.');
  //             }
  //         }
  //     });
  // }
</script>



<script>
    import Button from './UI/Button.svelte';
    //import { onMount } from "svelte";
    import {authenticate} from '../auth/auth';
    import { goto } from '@sapper/app';

    export let setAuthed;

  
    let email = '';
    let password = '';
    let passwordError;
    let emailError;
    let formErrors = [];
    const BASE_URL = 'http://localhost:8000';

    // const authenticate = payload => {
    //   return new Promise(async (resolve,reject) => {
    //     let message = '';
    //     const accessToken = localStorage.getItem('access_token');
    //         fetch(`${BASE_URL}/api/account/authenticate/`, 
    //             {
    //                 method: "POST",
    //                 mode: 'cors',
    //                 body: JSON.stringify(payload),
    //                 headers: { 
    //                     "Content-Type": "application/json",
    //                 }
    //             }
    //         ).then(res => {
    //             return res.json();
    //         })
    //         .then(data => {
    //             if(!data.access) {
    //               return reject(data.message);
    //             } else {
    //                 if(process.browser) {
    //                   console.log('Inside Browser')
    //                 }
    //                 localStorage.setItem('access_token',data.access);
    //                 localStorage.setItem('refresh_token',data.refresh);
    //                 return resolve('Successful');
    //             }
    //         })
    //         .catch(err => {
    //           return reject('An error occured trying to sign in.');
    //         });
    //     return reject('An error occured trying to sign in.');
    //   });
    // }

    function validateForm() {
        //clear
        formErrors = [];
        emailError = false;
        passwordError = false;
        let valid = true;
        if(email.trim() === '') {
            formErrors = [...formErrors,'You must enter a valid email address'];
            emailError = true;
            document.querySelector('#email').focus();
            valid = false
        }
        if(password.trim() === '') {
            formErrors = [...formErrors,'You must enter a value'];
            passwordError = true;
            document.querySelector('#password').focus();
            valid = false
        }
        return valid;
    }

    async function handleSignIn(e) {
      let message = '';
      e.preventDefault();
      if(validateForm()) {
        try {
          message = await authenticate({email,password});
          if(message === 'Successful') {
            console.log('Here');
            setAuthed(true);
          }
        } catch (err) {
          console.log(err);
        }
        
        console.log('I will sbmit this!', message);
      }
      console.log('Sign in happens here',email,password);
    }
</script>


<style>
/* forms */

.userForm {
  display: flex;
  flex-direction: column;
}

.formGroup {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin: 6px 0;
}

 /* sign in  */
 #signInForm {
   border: solid 1px #000;
   border-radius: 10px;
   padding: 1rem;
   margin: auto;
   max-height: 80vh;
   /* width: 36vw; */
   min-width: 30vw;
 }

 /* errors  */

 .formErrors {
   padding: 10px;
   max-width: 20vw;
 }

 /* .formErrors ul {
  list-style-type: square;
 }

 .formErrors ul li{
  color: var(--error-color);
 } */

 .formErrorInput {
   outline-color: var(--error-color);
   background-color: var(--form-error-bg);
 }

</style>


<form id="signInForm" class="userForm" onSubmit={handleSignIn} >
    <h1 class="centerText">Sign In</h1>
    <div class="formGroup">
        <label for="email">Email:</label>
        <input id="email" class={emailError ? "formErrorInput" : ""} type="email" bind:value="{email}" />
    </div>
    <div class="formGroup">
        <label for="password">Password:</label>
        <input id="password" class={passwordError ? "formErrorInput" : ""} type="password" bind:value="{password}" />
    </div>
    <Button className="btn btn-primary" on:click={handleSignIn} >SignIn</Button>
    <div class="formErrors">

    </div>
</form>