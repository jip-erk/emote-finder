<script>
  import logo from './assets/svelte.png'
 // import Counter from './lib/Counter.svelte'
  import EmoteGetter from './lib/GetEmote.svelte'

</script>

<main>
  
  <h1>emotes</h1>
  <hr class="solid">
  <EmoteGetter />


</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  

  main {
    text-align: center;
    
    margin: 0 auto;
    
  }


  h1 {
    
    text-transform: uppercase;
    font-size: 4rem;
    font-weight: 100;
    line-height: 1.1;
    margin: 1rem auto;
    max-width: 14rem;
  }



  @media (min-width: 480px) {
    h1 {
      max-width: none;
    }

    
  }
</style>
