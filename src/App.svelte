<script>
	import Tailwindcss from './Tailwindcss.svelte';
	import Router from 'svelte-spa-router'
import SignIn from './routes/SignIn.svelte';
import SignUp from './routes/SignUp.svelte';
import ForgotPassword from './routes/ForgotPassword.svelte';
import { promiseStore, userBaseStore, userStore } from './stores'	
	const userbase = window.userbase;
	window.userbase = null;

	// stores
	$userBaseStore = userbase;
	$userStore = null;
	
	$promiseStore = userbase.init({appId: '7b1dd005-660e-4e20-818d-f3250bb4955c'})
		.then(session => $userStore = session.user)

	function signout() {
		$promiseStore = $userBaseStore.signOut().then(() => $userStore = null )
	}	
		console.log($userStore)

</script>

<Tailwindcss />

<div 
	class="container flex flex-col justify-center items-center w-screen h-screen mx-auto ">
	{#await $promiseStore.then(() => Promise.reject()) }
			Loading...
	{:catch error}
			{#if error}
				<strong class="text-red-700 font-bold">Error ! {error} </strong>
			{/if}
		<!-- {:then _}  -->
		{#if $userStore }
			Hello, {$userStore.username} !
			<button on:click={signout} >Logout</button> 
		{:else}
			<Router routes={{
				// '/singup': SingUp,
					'/': SignUp,
				'/signin': SignIn,
				'/forgotpassword': ForgotPassword
			}} />
		
		{/if}
		
	{/await}
</div>
<!-- https://www.youtube.com/watch?v=LOZs0fpr4K4&t=4s&ab_channel=SvelteMastery -->