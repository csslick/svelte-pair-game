<script>
  // 카드정보 데이터
  const card_data = [
    {
      id: 0,
      name: 'html',
      imgUrl: 'images/html.png',
    },
    {
      id: 1,
      name: 'css',
      imgUrl: 'images/css.png',
    },
    {
      id: 2,
      name: 'js',
      imgUrl: 'images/js.png',
    },
    {
      id: 3,
      name: 'react',
      imgUrl: 'images/react.png',
    },
    {
      id: 4,
      name: 'vue',
      imgUrl: 'images/vue.png',
    },
    {
      id: 5,
      name: 'svelte',
      imgUrl: 'images/svelte.png',
    },
    {
      id: 6,
      name: 'sass',
      imgUrl: 'images/sass.png',
    },
    {
      id: 7,
      name: 'github',
      imgUrl: 'images/github.png',
    },
    {
      id: 8,
      name: 'quest',
      imgUrl: 'images/quest.png',
    },
  ]

  // 화면에 배치될 16장의 카드 목록
  // id:카드번호, flipped: 뒤집혀진 상태, matched: 매칭된 상태
  let cards = [
    { id: 0, flipped: true, matched: false },
    { id: 0, flipped: false, matched: false },
    { id: 1, flipped: false, matched: false },
    { id: 1, flipped: false, matched: false },
    { id: 2, flipped: false, matched: false },
    { id: 2, flipped: false, matched: false },
    { id: 3, flipped: false, matched: false },
    { id: 3, flipped: false, matched: false },
    { id: 4, flipped: false, matched: false },
    { id: 4, flipped: false, matched: false },
    { id: 5, flipped: false, matched: false },
    { id: 5, flipped: false, matched: false },
    { id: 6, flipped: false, matched: false },
    { id: 6, flipped: false, matched: false },
    { id: 7, flipped: false, matched: false },
    { id: 7, flipped: false, matched: false },
  ]

  // cards를 랜덤하게 섞기
  function shuffle() {
    cards = cards.sort(() => Math.random() - 0.5);
  }

</script>

<h1>game grid</h1>
<ul class="game-grid">
  {#each cards as card}
    <li class={card.flipped === true ? 'card flipped' : 'card'}>
      <img src={card_data[card.id].imgUrl} alt="" />
      <span style='position: absolute;'>{card.id},{card.flipped}</span>
    </li>
  {/each} 
</ul>
<button class='btn' on:click={shuffle}>reset</button>

<style lang="scss">
  .game-grid {
    // background: pink;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(4, 1fr);
    grid-gap: 2%;
    list-style-type: none;
    padding: 20px;

    .card {
      aspect-ratio: 1/1;
      background: #fff;
      border-radius: 18%;
      padding: 20%;
      img { 
        width: 100%;
        aspect-ratio: 1/1;
        object-fit: contain;
        display: block;
      }
    }
  }

  // 카드가 뒤집혀진 상태
  .game-grid .card.flipped {
    background: rgba(0,0,0, 0.5);
    img { display: none;}
    background-image: url('images/quest.png');
    background-repeat: no-repeat;
    background-size: 30%;
    background-position: center;
  }
</style>