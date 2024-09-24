<script>
    import { goto } from '$app/navigation';
    import {onMount} from 'svelte';
    import { page } from '$app/stores';
    
    let user = {};

    async function luu(){
        let res = await fetch(`http://10.0.2.14:3000/user/${$page.params.id}`, {
            method: "PUT",
            body: JSON.stringify(user),
            headers: {
                "Content-Type": "application/json"
            }
        });
        if(res.ok){
            goto('/quan-ly-nguoi-dung');
        }
        else{
            alert("That bai roi");
        }
        console.log(res);
    }

    onMount(async () => {
        const res = await fetch(`http://10.0.2.14:3000/user/${$page.params.id}`);
        user = await res.json();
        console.log(user);
    });
</script>

<form action="" on:submit={luu}>
    <label for="full-name">Ho va ten</label>
    <input id="full-name" type="text" bind:value={user.full_name}>
    <label for="username">Username</label>
    <input id="username" type="text" bind:value={user.username}>
    <label for="email">Email</label>
    <input id="email" type="email" bind:value={user.email}>
    <label for="password">Password</label>
    <input id="active" type="password" bind:value={user.password}>

    <button type="submit">Luu</button>
</form>