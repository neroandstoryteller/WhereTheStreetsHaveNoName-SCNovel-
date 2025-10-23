<script lang="ts">
    const novels = [
        { id: "/city/novel/jhonsWorkDiary", title: "Jhon's Work Diary" }
    ];
</script>

<h1 class="title">City · Novels</h1>

<section class="list">
    {#each novels as n}
        <a class="item" href={n.id} aria-label={n.title}>
            <span class="item-title">{n.title}</span>
        </a>
    {/each}
    </section>

<style>
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
        width: 100%;
        display: flex;
        flex-direction: column;
        gap: 14px;
        margin-top: 180px;
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

