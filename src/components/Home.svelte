<script>
	let promise = getPostData();
	async function getPostData() {
		const res = await fetch("https://jsonplaceholder.typicode.com/posts");
		const text = await res.text();
		if (res.ok) {
			return JSON.parse(text);
		} else {
			throw new Error(text);
		}
	}
</script>

<div class="flex-container">
{#await promise}
<div class="preloader-wrapper big active" style="margin: 200px auto;">
    <div class="spinner-layer spinner-teal-only">
      <div class="circle-clipper left">
        <div class="circle"></div>
      </div><div class="gap-patch">
        <div class="circle"></div>
      </div><div class="circle-clipper right">
        <div class="circle"></div>
      </div>
    </div>
</div>
{:then text}
	{#each text as item}
	<div class="flex-item">
		<div class="card teal">
			<div class="card-content white-text">
				<span class="card-title">{item.id} {item.title}</span>
				<p>{item.body}</p>
			</div>
			<div class="card-action">
				<a href="/article/{item.id}">Read</a>
			</div>
		</div>
	</div>
	{/each}
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}
</div>

<style>
.flex-container {
  display: flex;
  flex-flow: row wrap;
  justify-content: space-around; 
}

.flex-item {
  width: 300px;
  padding: 5px;
  margin-top: 5px;
  margin-bottom: 5px;
}
</style>