<script>
	import router from "page";
	import Home from './components/Home.svelte';
	import About from './components/About.svelte';
	import Article from './components/Article.svelte';

	let page;
	let params;

	router('/', () => page = Home);
	router('/about', () => page = About);
	router('/article/:id', (ctx, next) => {
  		params = ctx.params;
	  	next();
	  }, () => page = Article);
	router.start();
</script>

<svelte:head>
  <title>Blog App</title>
</svelte:head>


<nav>
  <div class="nav-wrapper">
    <a href="/" class="brand-logo">My Blog App</a>
    <ul id="nav-mobile" class="right hide-on-med-and-down">
      <li><a href="/">Home</a></li>
      <li><a href="/about">About</a></li>
        <!-- Login Random -->
      <li><a class='btn' href="#!">Login</a></li>
      <li><a class='btn' href="#!">Logout</a></li>
    </ul>
  </div>
</nav>

<svelte:component this={page} {params}/>

<footer class="page-footer">
  <div class="container">
    <div class="row">
      <div class="col l6 s12">
        <h5 class="white-text">Footer Content</h5>
        <p class="grey-text text-lighten-4">You can use rows and columns here to organize your footer content.</p>
      </div>
      <div class="col l4 offset-l2 s12">
        <h5 class="white-text">Tecnologias utilizadas:</h5>
        <ul>
          <li><a class="grey-text text-lighten-3" href="#!">Svelte 3</a></li>
          <li><a class="grey-text text-lighten-3" href="#!">Materializer</a></li>
          <li><a class="grey-text text-lighten-3" href="#!">Jsonplaceholder api</a></li>
        </ul>
      </div>
    </div>
  </div>
  <div class="footer-copyright">
    <div class="container">
    © 2020 Copyright
    <a class="grey-text text-lighten-4 right" href="http://www.github.com/jeferson0993/" target="_blank">Jeferson Ferreira</a>
    </div>
  </div>
</footer>

<style>
a {
  color: white;
  text-decoration: none;
}
.brand-logo {
  margin-left: 15px;
}
</style>