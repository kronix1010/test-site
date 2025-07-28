<script lang="ts">
  export let href = '/';
  export let label = 'Label';
</script>

<a {href} class="flex flex-col items-center">
  <svg
    class="w-[90px] h-[90px] fill-[#28447c]"
    viewBox="0 0 24 24"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      d="M19.5 6h-7.529l-1.942-2.394a1 1 0 0 0-.8-.406H4.5A2.5 2.5 0 0 0 2 5.5v13A2.5 2.5 0 0 0 4.5 21h15a2.5 2.5 0 0 0 2.5-2.5V8.5A2.5 2.5 0 0 0 19.5 6z"
    />
  </svg>
  <span class="font-['Quantico'] text-[24px] text-white">{label}</span>
</a>
