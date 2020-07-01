<script>
    import { onMount } from "svelte";
    export let params;	   
    console.log(params.id);
    let userRes = async function(){};
    let promise = getPostData();
	async function getPostData() {
		const res = await fetch("https://jsonplaceholder.typicode.com/posts/" + params.id);
		const text = await res.text();
		if (res.ok) {
            let userId = JSON.parse(text);
            let user = await fetch("https://jsonplaceholder.typicode.com/users/" + userId.userId);
            if (user.ok) {
                userRes = await user.text();
                userRes = JSON.parse(userRes);
                console.log('user: ', userRes);
            } else {
                throw new Error(text);
            }
			return JSON.parse(text);
		} else {
			throw new Error(text);
		}
	}
</script>

<h2>Article page</h2>
{#await promise}
	<p>...waiting</p>
{:then text}
	<h2>{text.id} - {text.title}</h2>
    <p>{text.body}</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}

{#await userRes}
    <p>...waiting</p>
{:then value}
    <p>{value.name}</p>
    <small>{value.phone}<br />{value.email}<br />{value.website}</small>
{:catch error}
    <small style="color: red">{error.message}</small>
{/await}