<script lang="ts">
  import { onMount, createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  let username = '';
  let password = '';

  const typewriter = (text: string, update: (val: string) => void, delay: number): Promise<void> => {
    return new Promise((resolve) => {
      let i = 0;
      const interval = setInterval(() => {
        if (i < text.length) {
          update(text.slice(0, i + 1));
          i++;
        } else {
          clearInterval(interval);
          resolve();
        }
      }, delay);
    });
  };

  onMount(async () => {
    const runAnimation = async () => {
      await typewriter('Alex Rodriguez', (val) => (username = val), 150);
      await new Promise((resolve) => setTimeout(resolve, 2000));
      await typewriter('**********', (val) => (password = val), 100);

      setTimeout(() => {
        dispatch('animationEnd');
      }, 500);
    };

    runAnimation();
  });
</script>

<div class="fixed inset-0 bg-[#28447c] flex items-center justify-center p-4">
  <div class="bg-gray-800 rounded-lg p-8 max-w-sm w-full">
    <div class="bg-gray-900 p-3 rounded h-10 font-mono mb-4 text-white">{username}</div>
    <div class="bg-gray-900 p-3 rounded h-10 font-mono text-white">{password}</div>
    <div class="flex justify-end gap-4 mt-6">
      <div class="text-white">Cancel</div>
      <div class="bg-blue-600 text-white px-4 py-2 rounded-lg">Log in</div>
    </div>
  </div>
</div>
