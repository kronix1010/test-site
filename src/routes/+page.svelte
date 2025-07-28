<script lang="ts">
  import Folder from '$lib/components/Folder.svelte';
</script>

<div class="min-h-screen bg-black md:flex md:items-center md:justify-center">
  <div
    class="w-full min-h-screen bg-[url('/images/kali-legacy.png')] bg-cover bg-right md:w-[1120px] md:min-h-0 md:aspect-[16/9] md:bg-center"
  >
    <div class="flex flex-col items-start gap-4 p-4 md:gap-5 md:p-10">
      <Folder label="Home" href="/" />
      <Folder label="Projects" href="/projects" />
      <Folder label="About" href="/about" />
    </div>
  </div>
</div>
