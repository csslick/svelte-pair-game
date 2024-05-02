<header class="game-info itim-regular">
  <dl>
    <div class='score'>
      <dt>Score</dt>
      <dd>999,999</dd>
    </div>
    <div class='round'>
      <dt>Round</dt>
      <dd>99</dd>
    </div>
    <div class='time'>
      <dt>Time</dt>
      <dd>100</dd>
    </div>
  </dl>
</header>

<style lang="scss">
  .game-info {
    position: absolute;
    left: 0;
    top: 0;
    width: 100vw;
    background: rgba(255,255,255,0.5);
    dl {
      display: flex;
      justify-content: space-between;
      padding: 10px 30px;
      dt { font-size: 3vw; }
      dd { font-size: 3vw; }
      // 글자 테두리 효과
      .round {
        color: #fff;
        -webkit-text-stroke: 6px rgba(0,0,0, 1);
        paint-order: stroke fill;
      }
      .score, .time {
        color: #fff;
        text-shadow: 2px 2px #000;
      }
    }
  }
</style>