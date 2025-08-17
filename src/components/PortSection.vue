<script setup>
import { onMounted, onUnmounted } from "vue";
import { portText } from "@/constants/index";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

let ctx;

const setupAnimation = () => {
    if (ctx) ctx.revert();

    ctx = gsap.context(() => {
        const portItems = document.querySelectorAll(".port__item");
        const portWrap = document.querySelector(".port__wrap");

        if (!portItems.length || !portWrap) return;

        // ★★★ React 버전과 동일한 애니메이션 로직 ★★★
        // 각 아이템들을 왼쪽으로 이동시켜 가로 스크롤 효과를 만듭니다.
        gsap.to(portItems, {
            xPercent: -100 * (portItems.length - 1),
            ease: "none",
            scrollTrigger: {
                trigger: "#port", // 애니메이션의 기준점
                pin: true,        // #port 섹션을 스크롤 동안 화면에 고정
                scrub: 1,         // 스크롤과 애니메이션을 부드럽게 동기화
                // end: 가로 스크롤이 끝나는 지점
                // 전체 가로 스크롤 거리 = (전체 너비 - 화면에 보이는 마지막 아이템 하나 너비)
                end: () => "+=" + (portWrap.offsetWidth - portItems[portItems.length - 1].offsetWidth),
                invalidateOnRefresh: true
            }
        });
    });
};

onMounted(() => {
    // 페이지의 모든 리소스(이미지 등)가 완전히 로드된 후 애니메이션 설정
    if (document.readyState === 'complete') {
        setupAnimation();
    } else {
        window.addEventListener('load', setupAnimation);
    }
});

onUnmounted(() => {
    // 컴포넌트가 사라질 때 모든 애니메이션과 이벤트 리스너 정리
    if (ctx) ctx.revert();
    window.removeEventListener('load', setupAnimation);
});
</script>

<template>
    <section id="port">
        <div class="port__inner">
            <div class="port__title">
                portfolio <em>포폴 작업물</em>
            </div>
            <div class="port__wrap">
                <div
                    v-for="(port, key) in portText"
                    :key="key"
                    :class="['port__item', `p${key + 1}`]"
                >
                    <span class="num">{{ port.num }}.</span>
                    <a :href="port.view" target="_blank" class="img">
                        <img :src="port.img" :alt="port.title" />
                    </a>
                    <h3 class="title">{{ port.title }}</h3>
                    <p class="desc">{{ port.desc }}</p>
                    <a :href="port.view" target="_blank" class="site">사이트 보기</a>
                </div>
            </div>
        </div>
    </section>
</template>

<style lang="scss">
    // 핵심 변경사항: React 버전과 동일하게 CSS를 구성합니다.
    #port {
        width: 100%;
        margin-top: 30vh;
        overflow: hidden; // 가로 스크롤바가 보이지 않도록 함
    }
    .port__inner {
        padding: 16px;
    }
    .port__title {
        position: relative; // pin이 적용된 섹션 내에서 z-index가 작동하도록
        z-index: 10;       // 스크롤되는 아이템들보다 위에 있도록 설정
        width: 100%;
        height: 5vw;
        font-size: 4vw;
        font-weight: 900;
        line-height: 1.6;
        font-family: var(--mainKor-font);
        text-transform: uppercase;
        color: var(--black100);
        border-bottom: 0.4vw solid var(--black100);
        margin-bottom: 16px;
        text-indent: -0.26vw;
    }
    .port__title em {
        font-size: 1.25rem;
        font-weight: 400;
        line-height: 2;
    }
    .port__wrap {
        display: flex;
        flex-wrap: nowrap; // 아이템들이 한 줄로 나열되도록
        width: 5200px;     // (아이템 너비 500 + 마진 20) * 10개 = 5200px
    }
    .port__item {
        flex-shrink: 0;   // 아이템 너비가 줄어들지 않도록
        width: 500px;
        height: 70vh;
        background-color: var(--subBg100);
        padding: 2.5rem;
        margin-right: 20px;
    }

    // 이하 나머지 스타일은 기존과 동일하게 유지
    .port__item.p1 { background-color: var(--subBg100); }
    .port__item.p2 { background-color: var(--subBg200); }
    .port__item.p3 { background-color: var(--subBg300); }
    .port__item.p4 { background-color: var(--subBg400); }
    .port__item.p5 { background-color: var(--subBg500); }
    .port__item.p6 { background-color: var(--subBg100); }
    .port__item.p7 { background-color: var(--subBg200); }
    .port__item.p8 { background-color: var(--subBg300); }
    .port__item.p9 { background-color: var(--subBg400); }
    .port__item.p10 { background-color: var(--subBg500); }

    .port__item .num { font-size: 2rem; font-family: var(--mainNum-font); }
    .port__item .img { display: block; margin-top: -20px; transition: margin-top 0.3s; }
    .port__item:hover .img { margin-top: 0; }
    .port__item .img img { border-radius: 5px; filter: saturate(0%); transition: all 0.3s; }
    .port__item .img:hover img { filter: saturate(100%) }
    .port__item .title { font-size: 1.5rem; text-align: center; padding: 0.8rem 0; font-weight: 700; color: var(--black100); border-bottom: 2px solid var(--black100); margin-bottom: 1rem; }
    .port__item .desc { font-size: 1rem; }
    .port__item .site { border: 1px solid var(--black100); display: block; text-align: center; padding: 0.625rem 1.5rem; margin-top: 1.5rem; }
</style>