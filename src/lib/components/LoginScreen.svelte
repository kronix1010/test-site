<script lang="ts">
  import { onMount, createEventDispatcher } from 'svelte';
  import { fade } from 'svelte/transition';

  const dispatch = createEventDispatcher();

  let username = '';
  let password = '';

  let mouseEl: SVGElement,
    usernameEl: HTMLDivElement,
    passwordEl: HTMLDivElement,
    loginButtonEl: HTMLDivElement;

  let mouseX = 0;
  let mouseY = 30;
  let isClicking = false;

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

  onMount(() => {
    const runAnimation = async () => {
      const sleep = (ms: number) => new Promise((resolve) => setTimeout(resolve, ms));

      const moveTo = async (element: HTMLElement) => {
        const rect = element.getBoundingClientRect();
        mouseX = rect.left + rect.width / 2;
        mouseY = rect.top + rect.height / 2;
        await sleep(700);
      };

      const click = async () => {
        isClicking = true;
        await sleep(200);
        isClicking = false;
      };

      // Animation sequence
      await moveTo(usernameEl);
      await click();
      await typewriter('Alex Rodriguez', (val) => (username = val), 100);

      await moveTo(passwordEl);
      await click();
      await typewriter('**********', (val) => (password = val), 50);

      await moveTo(loginButtonEl);
      await click();

      setTimeout(() => {
        dispatch('animationEnd');
      }, 500);
    };

    runAnimation();
  });
</script>

<div class="fixed inset-0 bg-[#28447c] flex items-center justify-center p-4">
  <!-- Mouse Pointer SVG -->
  <svg
    bind:this={mouseEl}
    style="position: absolute; left: {mouseX}px; top: {mouseY}px; transition: all 0.7s ease-in-out; z-index: 10;"
    class="w-6 h-6 {isClicking ? 'text-blue-300 scale-50' : 'text-white'}"
    xmlns="http://www.w3.org/2000/svg"
    viewBox="0 0 640 640"
    fill="currentColor"
    transition:fade
  >
    <!--!Font Awesome Free v7.0.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2025 Fonticons, Inc.-->
    <path d="M173.3 66.5C181.4 62.4 191.2 63.3 198.4 68.8L518.4 308.7C526.7 314.9 530 325.7 526.8 335.5C523.6 345.3 514.4 351.9 504 351.9L351.7 351.9L440.6 529.6C448.5 545.4 442.1 564.6 426.3 572.5C410.5 580.4 391.3 574 383.4 558.2L294.5 380.5L203.2 502.3C197 510.6 186.2 513.9 176.4 510.7C166.6 507.5 160 498.3 160 488L160 88C160 78.9 165.1 70.6 173.3 66.5z"/>
  </svg>

  <div class="bg-gray-800 rounded-lg p-8 max-w-sm w-full">
    <div bind:this={usernameEl} class="bg-gray-900 p-3 rounded h-10 font-mono mb-4 text-white">{username}</div>
    <div bind:this={passwordEl} class="bg-gray-900 p-3 rounded h-10 font-mono text-white">{password}</div>
    <div class="flex justify-end items-center gap-4 mt-6">
      <div class="text-white">Cancel</div>
      <div bind:this={loginButtonEl} class="bg-blue-600 text-white px-4 py-2 rounded-lg">Log in</div>
    </div>
  </div>
</div>
