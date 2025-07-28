<script lang="ts">
  import Folder from '$lib/components/Folder.svelte';
  import LoginScreen from '$lib/components/LoginScreen.svelte';
  import { fade } from 'svelte/transition';

  let showLogin = true;

  function handleAnimationEnd() {
    showLogin = false;
  }
</script>

<div class="bg-black">
  {#if showLogin}
    <LoginScreen on:animationEnd={handleAnimationEnd} />
  {:else}
    <div
      transition:fade={{ duration: 500, delay: 250 }}
      class="min-h-screen bg-[url('/images/kali-legacy.png')] bg-cover bg-[position:60%_center] md:bg-center"
    >
      <div class="flex flex-row justify-center items-start md:flex-col md:justify-start gap-4 p-4 md:gap-5 md:p-10">
        <Folder label="Home" href="/" />
        <Folder label="Projects" href="/projects" />
        <Folder label="About" href="/about" />
      </div>
    </div>
  {/if}
</div>
