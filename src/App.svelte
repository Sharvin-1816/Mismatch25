<script>
  import { onMount } from 'svelte';
  import BackgroundParticles from './BackgroundParticles.svelte';
  
  let countdown = { hours: 66, minutes: 21, seconds: 17 };

  function updateCountdown() {
    const now = new Date();
    const targetTime = new Date('2025-02-14T12:00:00');
    const timeDiff = targetTime.getTime() - now.getTime();
    const hours = Math.floor(timeDiff / (1000 * 60 * 60));
    const minutes = Math.floor((timeDiff % (1000 * 60 * 60)) / (1000 * 60));
    const seconds = Math.floor((timeDiff % (1000 * 60)) / 1000);
    countdown = { hours, minutes, seconds };
  }

  onMount(() => {
    updateCountdown();
    const timer = setInterval(updateCountdown, 1000);
    return () => clearInterval(timer);
  });
</script>

<svelte:head>
  <link href="https://fonts.googleapis.com/css2?family=Rubik:wght@400;500&family=Rubik+Glitch&display=swap" rel="stylesheet">
</svelte:head>

<main>
  <BackgroundParticles />
  <div class="content">
    <img src="/logo_trans.png" alt="IEEE RAS Logo" class="logo">
    <h1 style="font-weight: 200; font-size: 2rem">Presents</h1>
    <img src="/hackathon_logo_trans.png" alt="Hackathon Logo" class="hackathon-logo">
    <h1 style="font-weight: 200; font-size: 2.5rem">Launch In ...</h1>
    <div class="countdown">
      {countdown.hours}h  :  {countdown.minutes}m  :  {countdown.seconds}s
    </div>
  </div>
</main>

<style>
  main {
    min-height: 100vh;
    background-image: 
        linear-gradient(to right, rgba(255,255,255,0.1) 1px, transparent 1px),
        linear-gradient(to bottom, rgba(255,255,255,0.1) 1px, transparent 1px),
        radial-gradient(circle at bottom right, rgba(255,0,255,0.3) 0%, transparent 50%),
        radial-gradient(circle at top left, rgba(71, 5, 176, 0.3) 0%, transparent 50%);  /* Added indigo glow */
    background-size: 50px 50px, 50px 50px, 100% 100%, 100% 100%;  /* Size for all backgrounds */
    background-color: #000000;
    background-position: 0 0, 0 0, 0 0, 0 0;  /* Position for all backgrounds */
    background-repeat: repeat, repeat, no-repeat, no-repeat;  /* Grid repeats, but glows don't */
    position: relative;  /* Add this line */
}

  :global(body) {
      margin: 0;
      padding: 0;
      color: white;
      font-family: 'Rubik', sans-serif;
      overflow: hidden;
  }

  .logo {
    height: 100px;
    margin-right: auto;
    margin: 0 0.5rem;  /* Reduced margin around logo */
  }

  .hackathon-logo {
    max-width: 350px;  /* Reduced from 400px */
    animation: glitch 4s infinite;

}

h1 {
    font-family: 'Rubik Glitch', cursive;
    font-size: 2.3rem;   /* Reduced from 2.5rem */
    margin: 0;
    padding: 0;
}

.content {
    display: flex;
    flex-direction: column;
    align-items: center;
    position: relative;
    z-index: 2;
    justify-content: flex-start;  /* Changed from center to flex-start */
    min-height: calc(100vh - 80px);
    text-align: center;
    gap: 1rem;
    padding-top: 2%;  /* Add padding from the top to position the content higher */
}

  .countdown {
    font-family: 'Rubik Glitch', cursive;
    font-size: 4rem;
    color: #ffffff;  /* Add padding from the top */  
    font-weight: 200;
  }

  @keyframes glitch {
    0% {
        filter: none;
    }
    92% {
        filter: none;
    }   
    92.6% {
        filter: invert(0.1) hue-rotate(180deg);
        transform: translate(2px, 1px);
    }
    93% {
        filter: none;
        transform: none;
    }
    93.5% {
        filter: saturate(200%) brightness(150%);
        transform: translate(-2px, -1px);
    }
    94% {
        filter: none;
        transform: none;
    }
    94.5% {
        filter: hue-rotate(-90deg) contrast(150%);
        transform: translate(1px, -1px);
    }
    95% {
        filter: none;
        transform: none;
    }
    95.5% {
        filter: brightness(120%) contrast(150%);
        transform: translate(-1px, 1px) scale(1.01);
    }
    96% {
        filter: none;
        transform: none;
    }
}
</style>