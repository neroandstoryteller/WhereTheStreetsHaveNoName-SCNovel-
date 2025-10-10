<script lang="ts">
    const novels = [
        { id: 1, title: "서천고에서의 글" },
        { id: 2, title: "동곡고에서의 글" },
        { id: 3, title: "세 번째 묶음" },
        { id: 4, title: "네 번째 묶음" }
    ];
</script>

<div class="wrap">
    <div class="phone">
        <img
            src="/background.svg"
            alt="배경 일러스트"
            class="art"
        >
        <h1 class="title">Novel</h1>
    </div>

    <section class="list">
        {#each novels as n}
            <a class="item" href={"/novel/" + n.id} aria-label={n.title}>
                <span class="item-title">{n.title}</span>
            </a>
        {/each}
    </section>
</div>

<style>
    .wrap
    {
        box-sizing: border-box;
        width: 100%;
        min-height: 100dvh;
        padding: 24px 0 48px;
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 22px;
        background-color: #000000;
    }

    .phone
    {
        width: min(92vw, 420px);
        aspect-ratio: 9 / 19.5;
        border: 2px solid #222222;
        border-radius: 28px;
        overflow: hidden;
        position: relative;
        background-color: #ffffff;
        margin: 0 auto;
    }

    .art
    {
        position: absolute;
        inset: 0;
        width: 100%;
        height: 100%;
        object-fit: cover;
        display: block;
        pointer-events: none;
        user-select: none;
    }

    .title
    {
        position: absolute;
        left: 24px;
        top: 92px;
        margin: 0;
        font-size: clamp(20px, 3.4vw, 28px);
        font-weight: 700;
        color: #202020;
        letter-spacing: 0.2px;
    }

    .list
    {
        width: min(92vw, 420px);
        display: flex;
        flex-direction: column;
        gap: 14px;
    }

    .item
    {
        display: flex;
        align-items: center;
        justify-content: center;
        min-height: 88px;
        padding: 18px;
        border: 1.5px solid #cfcfcf;
        border-radius: 14px;
        background-color: #ffffff;
        text-decoration: none;
        transition: transform 120ms ease, box-shadow 120ms ease, border-color 120ms ease, background-color 120ms ease;
    }

    .item:hover
    {
        transform: translateY(-1px);
        border-color: #bdbdbd;
        box-shadow: 0 6px 16px rgba(0, 0, 0, 0.06);
        background-color: #fcfcfc;
    }

    .item-title
    {
        font-size: 15px;
        font-weight: 600;
        color: #333333;
        letter-spacing: 0.2px;
    }
</style>
