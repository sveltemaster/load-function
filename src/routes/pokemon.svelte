<script context="module">

  export async function load({page, fetch, session, context}) {
    console.log('pokemon load function!')
    // get query params
    let offset = page.query.get('offset') || '0'
    let limit = page.query.get('limit') || '20'
    const random = page.query.get('random')
    if (random) {
      offset = Math.floor(Math.random() * 500)
      limit = 50
    }
    const x = fetch('https://api.nativshark.com/api')

    // call pokemon api for list of pokemon
    const url = `https://pokeapi.co/api/v2/pokemon?offset=${offset}&limit=${limit}`
    const response = await fetch(url)
    const {results} = await response.json()
    // call pokemon api for each individual pokemon
    const pokemon = await Promise.all(results.map(({url}) => fetch(url).then(res => res.json())))
    
    return {
      props: {
        pokemon        
      },
      // maxage: 30
    }
  }
</script>

<script>
  export let pokemon
</script>

<h1>Pokemon</h1>

{#each pokemon as {name, sprites}}
  <div style="display: inline-block; padding: 0 2rem;">
    <h2>{name}</h2>
    <img src={sprites.front_default} alt={name}>
  </div>
{/each}