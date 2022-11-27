<script>
  import pomoLogo from './assets/pomoLogo.png'

  let diff = 0;
  let stopFlag = -1;
  let current = 0;
  let m = '0', s = '0';
  let ini;

  function stop(){
    stopFlag = 1;
    current = Date.now();
  }

  function start(){
    if(stopFlag == -1) {
      ini = Date.now();
      iniTimer();
      setInterval(iniTimer, 1000);
    }
    else if(stopFlag == 1){
      ini += Date.now() - current;
    }
    stopFlag = 0;
  }

  function iniTimer(){
    if(stopFlag == 0){
      diff = (25000 * 60) - (Date.now() - ini) // 현재 시간
      m = '0' + Math.floor(((diff / 1000) / 60));
      m = m.slice(m.length-2);
      s = '0' + Math.floor((diff / 1000) % 60);
      s = s.slice(s.length-2);
    }
  }
</script>

<main>
  <div>
    <img class="logo" src={pomoLogo}>
    <h1 style="color: red; margin: 0%">
      AmiPomodoro<br>
    </h1>
    <b>make your friend, pomodoro</b><br>
    <a>{m} : {s}</a>
  </div>
  <div>
    <button on:click={start}>
      <b>start</b>
    </button>
    <button on:click={stop}>
      <b>stop</b>
    </button>
  </div>
</main>

<style>
  .logo {
    height: 5.5em;
  }
</style>
