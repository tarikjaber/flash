<script lang="ts">
  let time = 600
  let timeLeft = time
  let pass = 0
  let miss = 0
  let startTime = new Date()
  Notification.requestPermission()
  
  setInterval(updateTime, 500)
  
  function updateTime() {
    let currentTime = new Date();
    let endTime = Math.floor(+startTime / 1000) + time;
    timeLeft = endTime - Math.floor(+currentTime / 1000);

    if (timeLeft <= 0) {
      new Notification("Time out!")
      startTime = new Date()
      miss += 1
      time = Math.floor(1.2 * time)
      timeLeft = time
    }
  }
  
  function formatTime(time: number) {
    let hours = Math.floor(time / 3600)
    let hourString = String(hours)
    let minutes = Math.floor(time / 60) - hours * 60
    let minuteString = String(minutes).padStart(2, '0')
    let seconds = time % 60
    let secondString = String(seconds).padStart(2, '0')
    
    if (hours > 0) {
     return hourString + ":" + minuteString + ":" + secondString 
    } else {
     return minuteString + ":" + secondString 
    }
  }
  
  function finish() {
    startTime = new Date()
    pass += 1
    time = Math.floor(time * 0.8)
    timeLeft = time
  }
</script>

<h1>{formatTime(timeLeft)}</h1>
<h3><span class="pass">{pass}</span> <span class="miss">{miss}</span></h3>
<button on:click={finish}>Done</button>

<style>
  h1 {
    margin: 0;
    margin-bottom: 0.1em;
  }
  
  button {
    background-color: #508D69;
  }
  
  .pass {
    color: #9ADE7B;
  }

  .miss {
    color: #FF8F8F;
  }
  
  h3 {
    font-size: 3em;
    margin: 0;
    margin-bottom: 0.6em;
  }
</style>
