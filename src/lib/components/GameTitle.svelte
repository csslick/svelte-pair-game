<script>
  import { onDestroy } from "svelte"; // ① 앱 종료시 라이프사이클 훅(오디오 정리용)
  import bgm from '../../assets/audio/bgm.mp3'; // ② bgm 추가
  import GamePlay from "./GamePlay.svelte";
  import GameScore from "./GameScore.svelte";

  export let title = "game title";
  let page = "title"; // title, play, score
  let audio = new Audio(bgm); // ③ 오디오 객체 생성

  // ④ 오디오 재생 함수
  function playAudio() {
    console.log('play audio');
    audio.loop = true;
    audio.volume = 0.8;
    audio.play();
  }

  // ⑤ 컴포넌트 종료시 audio 객체 삭제
  onDestroy(() => {
    audio.pause();
    audio = null;
  });
 
</script>

<main>
  <!-- paging logic -->
  {#if page === "title"}
    <section>
      <h1 class='itim-regular'>{title}</h1>
      <div class="btn-group">
        <button 
          on:click={() => {page ="play"; playAudio()}}
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