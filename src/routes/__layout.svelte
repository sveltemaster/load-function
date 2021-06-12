<script context="module">
  export async function load({page, fetch, session, context}) {
    return {
      props: {
        page
      },
      // context: {'message': 'sup'}
    }
  }
</script>

<script>
  export let page
</script>

<nav>
  <a href="/">Home</a>
  <a href="/pokemon?offset=0&limit=9">Starters Gen 1</a>
  <a href="/pokemon?offset=151&limit=9">Starters Gen 2</a>
  <a href="/pokemon?offset=251&limit=9">Starters Gen 3</a>
  <a href="/pokemon?offset=386&limit=9">Starters Gen 4</a>
  <a href="/pokemon?random=true">Random</a>
</nav>
<main>
  <slot />
</main>

<pre style="position: absolute; top: 1px; right: 1px;">{JSON.stringify(page, null, 2)}</pre>