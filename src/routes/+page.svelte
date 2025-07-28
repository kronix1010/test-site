<script lang="ts">
  import Folder from '$lib/components/Folder.svelte';
</script>

<div class="min-h-screen bg-[url('/images/kali-legacy.png')] bg-cover bg-center">
  <div class="flex flex-col items-start gap-5 p-10">
    <Folder label="Home" href="/" />
    <Folder label="Projects" href="/projects" />
    <Folder label="About" href="/about" />
  </div>
</div>
