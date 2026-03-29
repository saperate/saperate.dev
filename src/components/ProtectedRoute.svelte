<script>
    import { onMount } from "svelte";
    import {goto} from "$app/navigation";
    
    async function validateSession() {
        try {
            const response = await fetch("/validate", {
                credentials: "include",
            });
            return response.ok;

        } catch (error) {
            return false;
        }
    }

    onMount(async () => {
        if(!await validateSession()){
            goto("/auth");
        }
    })
</script>

<slot/>