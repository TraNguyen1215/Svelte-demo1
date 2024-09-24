<script>
    import { onMount } from 'svelte';

    let users = [];

    async function xoa(id){
        if (confirm("Ban co chac chan muon xoa?")) {
            let res = await fetch(`http://10.0.2.14:3000/user/${id}`, {
            method: "DELETE",
            });
            if(res.ok) {
                alert("Xoa thanh cong");
            } else {
                alert("Xoa that bai");
            }
        }
    }    
    onMount(async () => {
    const rest = await fetch(`http://10.0.2.14:3000/user`);
    users = (await rest.json()).data;
    console.log(users);
    });
</script>

<!-- {#each users as user, i (i)}
    {JSON.stringify(user)}
{/each} -->
<a href="/quan-ly-nguoi-dung/them">Them moi</a>
<table>
    <thead>
        <tr>
            <th>STT</th>
            <th>Họ và tên</th>
            <th>Username</th>
            <th>Email</th>
            <th>Trạng thái</th>
            <th>Sửa</th>
        </tr>
    </thead>
    <tbody>
        {#each users as user, i (i)}
            <tr>
                <td>{i + 1}</td>
                <td>{user.full_name}</td>
                <td>{user.username}</td>
                <td>{user.email}</td>
                <td>{user.active}</td>
                <td>
                    <a href="/quan-ly-nguoi-dung/{user.id}/sua">Sửa</a>
                </td>
                <td>
                    <a href={"#"} on:click={() => xoa(user.id)}>Xóa</a>
                </td>
            </tr>
        {/each}
    </tbody>
</table>
