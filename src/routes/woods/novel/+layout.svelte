<script lang="ts">
    let { children } = $props();
</script>

<div class="novel-fade">
    {@render children?.()}
</div>

<style>
    .novel-fade { opacity: 0; animation: novel-fade-in 800ms ease-out 2.2s forwards; }
    @keyframes novel-fade-in { from { opacity: 0; transform: translateY(4px); } to { opacity: 1; transform: translateY(0); } }
    @media (prefers-reduced-motion: reduce) { .novel-fade { animation: none; opacity: 1; } }
</style>

