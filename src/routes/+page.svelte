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
      class="min-h-screen bg-[url('/images/kali-legacy.png')] bg-cover bg-center"
    >
      <div class="flex flex-col items-start gap-4 p-4 md:gap-5 md:p-10">
        <Folder label="Home" href="/" />
        <Folder label="Projects" href="/projects" />
        <Folder label="About" href="/about" />
      </div>
    </div>
  {/if}
</div>
