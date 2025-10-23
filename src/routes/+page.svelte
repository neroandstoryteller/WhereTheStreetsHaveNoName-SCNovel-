<script lang="ts">
    const links = [
        { href: '/city', label: 'City' },
        { href: '/woods', label: 'Woods' }
    ];
    let { data } = $props();
</script>

<h1 class="title">Where The Streets Have No Name</h1>

<nav class="nav">
    {#each links as l}
        <a class="nav-btn" href={l.href} aria-label={l.label}>{l.label}</a>
    {/each}
    </nav>

<style>
    .title
    {
        margin: 28px 0 16px 0;
        text-align: center;
        font-weight: 800;
        font-size: clamp(22px, 5vw, 34px);
        letter-spacing: .4px;
        color: #222;
    }

    .nav
    {
        display: flex;
        justify-content: center;
        gap: 14px;
        padding: 20px;
    }

    .nav-btn
    {
        display: inline-flex;
        align-items: center;
        justify-content: center;
        min-width: 140px;
        padding: 14px 18px;
        border-radius: 12px;
        text-decoration: none;
        color: #fff;
        background: linear-gradient(180deg, #4c7fff, #3461d8);
        box-shadow: 0 8px 18px rgba(52,97,216,.25);
        transition: transform 120ms ease, box-shadow 120ms ease, filter 120ms ease;
    }

    .nav-btn:hover { transform: translateY(-1px); filter: brightness(1.05); box-shadow: 0 12px 24px rgba(52,97,216,.28); }
    .nav-btn:active { transform: translateY(0); filter: brightness(.98); }
</style>

