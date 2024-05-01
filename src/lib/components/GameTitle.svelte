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
      <h1>{title}</h1>
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
    <GameScore />
  {/if}
</main>