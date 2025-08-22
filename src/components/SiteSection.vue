<script setup>
// 사이트 섹션에 표시할 데이터를 가져옵니다
import { siteText } from "@/constants/index";
</script>

<template>
    <!-- 사이트 코딩 섹션: 작업물을 소개하는 섹션 -->
    <section id="site">
        <div class="site__inner">
            <!-- 섹션 제목 -->
            <h2 class="site__title">
                Site coding <em>나의 작업물</em>
            </h2>
            <!-- 사이트 아이템 리스트 컨테이너 -->
            <div class="site__wrap">
                <!-- 각 사이트 아이템을 반복하여 표시 -->
                <div class="site__item" v-for="(site, key) in siteText" :key="key">
                    <!-- 아이템 번호 -->
                    <span class="num">{{ key + 1 }}.</span>
                    <!-- 사이트 설명 텍스트 -->
                    <div class="text">
                        <div>{{ site.text[0] }}</div>
                        <div>{{ site.text[1] }}</div>
                        <div>{{ site.text[2] }}</div>
                    </div>
                    <!-- 사이트 제목 -->
                    <h3>
                        {{ site.title }}
                    </h3>
                    <!-- 코드와 뷰 버튼 -->
                    <div class="btn">
                        <a :href="site.code">code</a>
                        <a :href="site.view">view</a>
                    </div>
                    <!-- 추가 정보 -->
                    <div class="info">
                        <span>{{ site.info[0] }}</span>
                        <span>{{ site.info[1] }}</span>
                        <span>{{ site.info[2] }}</span>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template> 

<style lang="scss" scoped>
@use "@/assets/scss/mixin" as *;

/* 사이트 섹션 내부 컨테이너 */
.site__inner {
    padding: 16px;

    /* 사이트 섹션 제목 스타일링 */
    .site__title  {
        position: sticky; /* 스크롤 시 제목을 고정 */
        top: 70px;
        left: 0;
        width: 70%;
        height: 5vw;
        font-size: 4vw;
        font-weight: 900;
        line-height: 1.6;
        font-family: var(--mainKor-font);
        text-transform: uppercase;
        color: var(--black100);
        border-bottom: 0.4vw solid var(--black100);
        margin-bottom: 100px;

        /* 모바일 화면에서의 제목 스타일 */
        @media (max-width: 800px){ 
            width: 100%;
            margin-bottom: 10vw;
            font-size: 30px;
            height: auto;
            top: 68px;
            z-index: 1000;
            background-color: var(--mainBg-color);
        }

        /* 제목 내 강조 텍스트 */
        em {
            font-size: 1.25rem;
            font-weight: 400;
            line-height: 2;
        }
    }
    /* 사이트 아이템 리스트 컨테이너 */
    .site__wrap {
        /* 각 사이트 아이템 */
        .site__item {
            height: 70vh;
            @include flex-center; /* 콘텐츠 가운데 정렬 */
            flex-direction: column;
            position: sticky; /* 스크롤 시 아이템 고정 */
            left: 0;

            /* 첫 번째 사이트 아이템 */
            &:nth-child(1) {
                background-color: var(--subBg100);
                top: 180px; /* 스크롤 시 고정되는 위치 */

                @media (max-width: 800px){ 
                    top: 140px;
                }
            }
            /* 두 번째 사이트 아이템 */
            &:nth-child(2) {
                background-color: var(--subBg200);
                top: 200px; /* 스크롤 시 고정되는 위치 */

                @media (max-width: 800px){ 
                    top: 160px;
                }
            }
            /* 세 번째 사이트 아이템 */
            &:nth-child(3) {
                background-color: var(--subBg300);
                top: 220px; /* 스크롤 시 고정되는 위치 */

                @media (max-width: 800px){ 
                    top: 180px;
                }
            }
            /* 네 번째 사이트 아이템 */
            &:nth-child(4) {
                background-color: var(--subBg400);
                top: 240px; /* 스크롤 시 고정되는 위치 */

                @media (max-width: 800px){ 
                    top: 200px;
                }
            }
            /* 번호 스타일링 */
            .num {
                font-size: 5vw;
                line-height: 1;
                font-weight: 900;
                font-family: var(--mainNum-font);
                position: absolute; /* 절대 위치로 배치 */
                left: 1vw;
                top: 1vw;

                @media (max-width: 800px) and (min-width: 481px) { 
                    font-size: 60px;
                    left: 15px;
                    top: 15px;
                }
                
                @media (max-width: 480px) { 
                    font-size: 50px;
                    left: 10px;
                    top: 10px;
                }
                
                @media (max-width: 320px) { 
                    font-size: 40px;
                    left: 8px;
                    top: 8px;
                }
            }
            /* 텍스트 스타일링 */
            .text {
                text-align: center;
                margin-bottom: 1rem;

                /* 텍스트 내부 요소 */
                > div {
                    font-size: 3vw;
                    line-height: 1;
                    font-weight: 900;
                    text-transform: uppercase;
                    text-decoration: underline;
                    font-family: var(--mainEng-font);

                    @media (max-width: 800px) and (min-width: 481px) { 
                        font-size: 30px;
                    }
                    
                    @media (max-width: 480px) { 
                        font-size: 22px;
                    }
                    
                    @media (max-width: 320px) { 
                        font-size: 18px;
                    }
                }
            }
            /* 제목 스타일링 */
            .title {
                font-family: var(--mainKor-font);
                margin-bottom: 1rem;
            }
            /* 버튼 스타일링 */
            .btn {
                /* 버튼 링크 */
                a {
                    text-decoration: underline;
                    text-transform: uppercase;
                    color: var(--black200);
                    font-size: 1rem;
                    transition: all 0.3s;
                    margin: 0 2px;

                    &:hover {
                        color: var(--black);
                    }
                }
            }
            /* 추가 정보 스타일링 */
            .info {
                position: absolute; /* 절대 위치로 배치 */
                left: 0;
                bottom: 3%;
                width: 98%;
                margin-left: 1%;
                border-top: 1px solid var(--black);
                border-bottom: 1px solid var(--black);
                display: flex;
                justify-content: space-between;

                @media (max-width: 800px){ 
                    flex-direction: column;
                    width: 90%;
                    margin-left: 5%;
                    padding: 5px 0;
                }

                /* 정보 항목 */
                span {
                    font-family: var(--mainKor-font);
                    font-size: 12px;
                    padding: 3px 0;
                    text-transform: uppercase;
                }
            }
        }
    }
}
</style>