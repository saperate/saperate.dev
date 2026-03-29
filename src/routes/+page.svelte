<script lang="ts">
	import {type User} from "@teamhanko/hanko-elements";
	import {onMount} from "svelte";
	import {getUserOrUndefined} from "$lib/browser/auth";
	
	let user : User | undefined = undefined;
	onMount(async () => {
		user = await getUserOrUndefined();
	});
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>
THIS IS MAIN
{user === undefined || user.username === undefined ? "" : "Hello " + user.username.username + "!!!"}

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
	
	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}
</style>
