<script>
    import { onMount } from "svelte";
    import {goto} from "$app/navigation";
    import {getHanko} from "$lib/browser/auth.js";
    
    async function validateSession() {
        try {
            const hanko = await getHanko();
            return (await hanko.validateSession()).is_valid;
        } catch (error) {
            return false;
        }
    }

    onMount(async () => {
        if(!await validateSession()){
            await goto("/auth");
        }
    })
</script>

<slot/>