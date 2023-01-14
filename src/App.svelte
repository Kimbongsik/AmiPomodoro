<script>
  import pomoLogo from './assets/pomoLogo.png'
  
  //name
  let name = '';
  let status = '';

  //counter
  let cnt = 0;

  //timer
  let diff = 0;
  let startFlag = 0;
  let stopFlag = -1;
  let current = 0;
  let m = '00', s = '00';
  let ini;

  function stop(){
    stopFlag = 1;
    current = Date.now();
  }

  function start(){
    document.body.style.backgroundColor = "#dc143c";
    if(stopFlag == -1) {
      startFlag = 1;
      status = "Work";
      ini = Date.now();
      iniTimer();
      if(!(m=='00' && s=='01')){
        setInterval(iniTimer, 100);
        cnt++;
      }
    }
    
    else if(stopFlag == 1){
      ini += Date.now() - current;
    }
    stopFlag = 0;
  }

  function iniTimer(){
    if(stopFlag == 0){
      diff = (50 * 60) - (Date.now() - ini) // 현재 시간
      if (diff >= 0){
        m = '0' + Math.floor(((diff / 1000) / 60));
        m = m.slice(m.length-2);
        s = '0' + Math.floor((diff / 1000) % 60);
        s = s.slice(s.length-2);
      }

      else if(diff < 0){
        stopFlag = -1;
      }
    }

    if(stopFlag == 0 && m=='00' && s=='00'){
      status = "Break";
      document.body.style.backgroundColor = "#14a0dc";
    }
  }

</script>

<main>
  <div>
    <img class="logo" src={pomoLogo}>
    <h1 style="margin: -5%">
      <p>AmiPomodoro</p>
    </h1>
    <p style="font-style:italic; font-weight: bold">make your friend, pomodoro</p>
    <p style="margin-top: 5%; font-size: 3rem; font-weight:bold"> {status}, {name}.</p>
    <input type="text" bind:value={name}/>

    <p style="font-style:italic; font-weight: bold">#{cnt}</p>
  
  </div>

  <div>
    <p class="time">{m}:{s}</p>
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
    height: 8em;
    margin: 0 auto;
  }
  .time{
    font-weight:bold;
    font-size:15rem;
    margin-top: 1;
    margin-bottom: 1;
    margin-left: 100;
    margin-right: 100;
  }
</style>
