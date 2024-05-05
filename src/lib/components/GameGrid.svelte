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
    { id: 0, flipped: false, matched: false },
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


  // 카드 섞기 함수
  function shuffle() {
    stageClear = false; // 게임 클리어 상태 초기화
    cards = cards.sort(() => Math.random() - 0.5); // cards를 랜덤하게 섞기

    // 카드 상태 초기화
    cards.forEach(card => {
      card.flipped = false;
      card.matched = false;
    })
  }

  // 카드 뒤집기
  function handleCard(i) { // i = cards 배열값
    if (cards[i].flipped === false) {
      cards[i].flipped = true;
    };
    
    // 1초 후 카드 닫음
    setTimeout(() => {
      cards[i].flipped = false;
    }, 1000);
    
    // 카드 매칭 체크
    checkMatch(i); // 카드 위치값을 전달하여 게임판정
  }

  let pairArr = [null, null]; // 매칭된 카드 번호를 저장하는 배열

  // 게임 클리어 상태변수
  let stageClear = false; 

  // 카드 매칭 체크
  function checkMatch(i) {
    // 카드 위치가 다를 때만 추가
    if(pairArr[1] !== i) {
      pairArr.shift(); // 이전 배열값 삭제
      pairArr.push(i); // 현재 배열값 추가
    }

    // 카드 일치 판정
    if(
      cards[pairArr[0]]?.id === cards[pairArr[1]].id 
      &&
      cards[pairArr[0]]?.flipped // 카드가 열려있을 때만 판정
    ) {
      cards[pairArr[0]].matched = true;
      cards[pairArr[1]].matched = true;
    }

    // 모든 카드의 짝을 찾으면 게임 클리어
    stageClear = cards.every(card => card.matched === true);

    console.log(pairArr); 
    // console.log(cards[pairArr[0]], cards[pairArr[1]])
  } 


</script>

<!-- <h1>game grid</h1> -->
<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
<ul class="game-grid">
  {#each cards as card, i}
    <li 
      on:click={() => handleCard(i)}  
      class={card.flipped || card.matched === true ? 'card' : 'card hidden'}
    >
      <img src={card_data[card.id].imgUrl} alt="" />
      <span style='position: absolute;'>
        {card.id},{card.flipped},{card.matched}
      </span>
    </li>
  {/each} 
</ul>

<!-- 게임 클리어 모달 창 -->
{#if stageClear}
  <div class="modal">
    <div class="modal-container">
      <h1>Game Clear!</h1>
      <p class='bonus-score-title'>Bonus score</p>
      <p class='bonus-score'>5,000</p>
      <button class='btn next' on:click={shuffle}>Next</button>
      <button class="btn" on:click={() => { 
        // home으로 돌아가기
      }}>Home</button>
    </div>
  </div>
{/if}

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
  .game-grid .card.hidden {
    background: rgba(0,0,0, 0.5);
    img { opacity: 0; }
    background-image: url('images/quest.png');
    background-repeat: no-repeat;
    background-size: 30%;
    background-position: center;
  }

  // 모달창 스타일
  .modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0,0,0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 100;
    display: grid;
    place-items: center;

    .modal-container {
      background: #fff;
      width: 400px;
      padding: 20px;
      border-radius: 30px;
      border: 10px solid #000;
      h1 { margin-bottom: 5px; }
      .bonus-score-title {
        font-size: 20px;
        color: #666;
      }
      .bonus-score {
        font-size: 36px;
        color: #f63030;
        margin-bottom: 20px;
      }
    }

    .btn { 
      font-size: 24px; 
      &.next { color: #f63030; }
    }
  }
</style>