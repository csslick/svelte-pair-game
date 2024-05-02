<script>
  import GamePlay from "./GamePlay.svelte";
  import GameScore from "./GameScore.svelte";

  export let title = "game title";
  let page = "title"; // title, play, score
</script>

<main>
  <!-- paging logic -->
  {#if page === "title"}
    <section>
      <h1 class='itim-regular'>{title}</h1>
      <div class="btn-group">
        <button 
          on:click={() => page ="play"}
        >Start</button>
        <button
          on:click={() => page="score"}
        >Score</button>
      </div>
    </section>
  {:else if page === "play"}
    <GamePlay />
  {:else if page === "score"}
    <GameScore bind:page={page} />
  {/if}
</main>

<style lang="scss">
  section {
    h1 { 
      font-size: 16vw; 
      color: #ff3e00;
      -webkit-text-stroke: 10px rgba(0,0,0, 0.5);
      paint-order: stroke fill;
    }
  }
  .btn-group {
    display: flex;
    flex-direction: column;
    margin-top: 40px;
    button { 
      padding: 10px;
      font-size: 32px;
      background: transparent;
      border: none;
      &:hover { text-decoration: underline;}
    }
  }
</style>