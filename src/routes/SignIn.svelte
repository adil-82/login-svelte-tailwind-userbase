<script>
    import A from "../components/A.svelte";
import Button from "../components/Button.svelte";
    import Input from "../components/Input.svelte";
import { promiseStore, userBaseStore, userStore } from "../stores";

    let username, password

    function signin() {
        $promiseStore = $userBaseStore.signIn({ username, password })
            .then( user => $userStore = user )
    }

    console.log($userStore)

</script>

<form on:submit|preventDefault={signin} 
    class="lg:w-2/6 md:w-1/2 bg-gray-100 rounded-lg p-8 flex flex-col w-full mt-10 md:mt-0">
    <div class="flex justify-between">
        <h2 class="text-gray-900 text-lg font-medium title-font mb-5">Sign In</h2>
        <A href="/">Or...Sign Up</A>
    </div>  
    
      <Input label="Username" type="username" bind:value={username} require />
      <Input label="Password" type="password" bind:value={password} require />
      <Button>Sing In !</Button>
      <p class="text-xs text-gray-500 mt-3">
        <A href="/#/forgotpassword">Forgot Password ?</A>
      </p>
</form>