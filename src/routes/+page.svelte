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
<!-- TODO add a page for donations/commissions, commissions would probably just redirect them to my discord or send a mail -->