<script lang="ts">
    import { onMount } from 'svelte';
    import Story from './Story.svelte';
    import './story.css';

    let audioEl: HTMLAudioElement;
    let heroEl: HTMLElement;
    let isPlaying = false;

    function tryPlay() {
        if (!audioEl) return;
        const p = audioEl.play();
        if (p && typeof (p as any).then === 'function') {
            (p as Promise<void>).then(() => {
                isPlaying = true;
            }).catch(() => {
                /* autoplay may be blocked; wait for user gesture */
            });
        } else {
            isPlaying = !audioEl.paused;
        }
    }

    function pause() {
        if (!audioEl) return;
        audioEl.pause();
        isPlaying = false;
    }

    onMount(() => {
        if (audioEl) {
            audioEl.preload = 'auto';
            audioEl.volume = 1;
        }

        const resume = () => {
            tryPlay();
            window.removeEventListener('pointerdown', resume);
            window.removeEventListener('keydown', resume);
        };
        window.addEventListener('pointerdown', resume, { once: true });
        window.addEventListener('keydown', resume, { once: true });

        const observer = new IntersectionObserver(
            (entries) => {
                for (const e of entries) {
                    if (e.target === heroEl && e.intersectionRatio < 0.1) {
                        tryPlay();
                    }
                }
            },
            {
                root: document.querySelector('.viewport') as Element | null,
                threshold: [0, 0.1, 0.5, 1]
            }
        );
        if (heroEl) observer.observe(heroEl);

        const onVis = () => { if (document.hidden) pause(); };
        document.addEventListener('visibilitychange', onVis);

        return () => {
            observer.disconnect();
            document.removeEventListener('visibilitychange', onVis);
        };
    });
</script>

<section class="hero" bind:this={heroEl} aria-label="소설 서문">
    <h1 class="title">모순</h1>

    <img src='/tropical.jpg' class="tropical" alt="tropical" >
    <button class="player" type="button" aria-label={isPlaying ? '음악 일시정지' : '음악 재생'} on:click={() => (isPlaying ? pause() : tryPlay())}>
        <div class="record" class:spinning={isPlaying} aria-hidden="true"></div>
        <div class="meta">
            <div class="track">Last Carnival</div>
            <div class="state">{isPlaying ? '재생 중' : '대기 중'}</div>
        </div>
        <audio
            bind:this={audioEl}
            src="/Last Carnival.mp3"
            on:play={() => (isPlaying = true)}
            on:pause={() => (isPlaying = false)}
        ></audio>
    </button>
    <div class="hint">아래로 내려 읽기를 시작하세요</div>
    <div class="spacer" aria-hidden="true"></div>
    <!-- sentinel space so the user scrolls past the hero before content -->
</section>

<article class="content">
    <p>
        그녀가 죽어선 안돼. 죽지 말아줘. 제발 죽지 말아줘. 그녀가 없는 세상을 살고 싶지 않아.
        살고 싶지 않아. 죽어야만 해. 차라리 같이 죽자.
    </p>
    <p>
        이 이야기를 하는 건 당신이 처음입니다. 네네, 모두 이야기 해드리겠습니다. 그녀는... 그녀는...
        아아, 말이 잘 나오지 않습니다. 미안합니다.
    </p>
</article>

<Story />

<style>
    :global(body) { font-size: 1rem; }


    .tropical {
        width: 100%;         /* 가로를 화면 전체에 맞춤 */
        height: auto;         /* 세로는 비율에 따라 자동 */
        display: block;
        margin: 0 auto;
        object-fit: contain;  /* 이미지 왜곡 방지 (선택 사항) */
    }

    .hero {
        display: grid;
        gap: 14px;
        padding: 18px 6px 8px 6px;
        text-align: center;
    }

    .title {
        margin: 0;
        font-size: clamp(28px, 6vw, 36px);
        font-weight: 800;
        letter-spacing: 0.5px;
        color: #222;
        text-shadow: 0 1px 0 rgba(255,255,255,0.6);
    }

    .player {
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 12px;
        padding: 10px 12px;
        border: 1px solid #e0e0e0;
        border-radius: 9999px;
        background-color: #ffffffd9;
        box-shadow: 0 4px 12px rgba(0,0,0,0.06);
        user-select: none;
        cursor: pointer;
    }

    .record {
        width: 32px;
        height: 32px;
        border-radius: 50%;
        background:
            radial-gradient(circle at 50% 50%, #222 0 8px, transparent 9px),
            repeating-radial-gradient(circle at 50% 50%, #444 0 2px, #111 2px 4px);
        box-shadow: inset 0 0 0 2px #000, 0 1px 3px rgba(0,0,0,0.2);
        animation: spin 3.6s linear infinite;
        animation-play-state: paused;
    }
    .record.spinning { animation-play-state: running; }
    @keyframes spin { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }

    .meta { display: grid; line-height: 1.1; }
    .track { font-weight: 700; font-size: 0.95rem; color: #1f1f1f; }
    .state { font-size: 0.78rem; color: #686868; }

    .hint {
        font-size: 0.9rem;
        color: #555;
    }

    .spacer { height: 28px; }

    .content {
        padding: 6px;
        color: #1e1e1e;
        line-height: 1.7;
        word-break: keep-all;
    }

    .content p { margin: 0 0 18px 0; }
</style>