<script lang="ts">
	import {Hanko, NotFoundError, type User} from "@teamhanko/hanko-elements";
	import {onMount} from "svelte";
	import {goto} from "$app/navigation";

	const hankoApi = import.meta.env.VITE_HANKO_API_URL;
	
	let user : User | undefined = undefined;
	
	async function fetchUserData() {
		const hanko = new Hanko(hankoApi);
		return await hanko.getCurrentUser();
	}
	onMount(async () => {
		let data;
		try{
			data = await fetchUserData();
		}catch (e) { //We were not authorised or there was a technical error, either way go back to homepage
			goto("/")
			return;
		}
		user = data;
	});
	
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>
THIS IS MAIN
{#if user !== undefined}
	Hello, {user.name}!!!
{/if}

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}

	.welcome {
		display: block;
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}
</style>
