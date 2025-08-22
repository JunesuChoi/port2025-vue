<script setup>
// 사이트 섹션에 표시할 데이터를 가져옵니다
import { siteText } from "@/constants/index";
// R&D 포털 이미지 import
import rdPortalImg from "@/assets/img/rd-portal.jpg";
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
                <div class="site__item" v-for="(site, key) in siteText" :key="key" 
                     :class="{ 'rd-portal': key === 1 }"
                     :style="key === 1 ? { backgroundImage: `linear-gradient(rgba(102, 126, 234, 0.85), rgba(118, 75, 162, 0.85)), url(${rdPortalImg})` } : {}">
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
    
    /* 충분한 스크롤 공간 확보 */
    .site__wrap {
        padding-bottom: 100vh; /* 마지막 카드가 완전히 표시되도록 */
    }

    /* 사이트 섹션 제목 스타일링 */
    .site__title  {
        position: sticky; /* 스크롤 시 제목을 고정 */
        top: 70px;
        left: 0;
        width: 100%;
        height: auto;
        font-size: 4vw;
        font-weight: 900;
        line-height: 1.2;
        font-family: var(--mainEng-font);
        text-transform: uppercase;
        color: var(--text-primary);
        background: var(--mainBg-color);
        border-bottom: 3px solid var(--primary-color);
        margin-bottom: 50px;
        padding: 20px 16px;
        z-index: 10;

        /* 모바일 화면에서의 제목 스타일 */
        @media (max-width: 800px){ 
            font-size: 2rem;
            padding: 16px;
            top: 60px;
            margin-bottom: 30px;
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
            height: 80vh;
            min-height: 600px;
            @include flex-center; /* 콘텐츠 가운데 정렬 */
            flex-direction: column;
            position: sticky; /* 스크롤 시 아이템 고정 */
            left: 0;
            border-radius: 20px;
            margin: 0 16px 40px 16px; /* 하단 여백 추가 */
            transition: all 0.3s ease;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3);
            
            &:hover {
                transform: translateY(-3px);
                box-shadow: 0 25px 50px rgba(0, 0, 0, 0.4);
                
                &:nth-child(1) { 
                    border-color: var(--primary-color);
                    box-shadow: 0 25px 50px rgba(0, 212, 255, 0.3);
                }
                &:nth-child(2) { 
                    border-color: var(--secondary-color);
                    box-shadow: 0 25px 50px rgba(255, 107, 107, 0.3);
                }
                &:nth-child(3) { 
                    border-color: var(--accent-color);
                    box-shadow: 0 25px 50px rgba(78, 205, 196, 0.3);
                }
                &:nth-child(4) { 
                    border-color: var(--warning-color);
                    box-shadow: 0 25px 50px rgba(255, 217, 61, 0.3);
                }
            }

            /* 첫 번째 사이트 아이템 - 가장 아래 위치 */
            &:nth-child(1) {
                background: var(--cardBg-color);
                border: 1px solid rgba(0, 212, 255, 0.2);
                top: 70px; /* 가장 위에 고정 */
                z-index: 4;

                @media (max-width: 800px){ 
                    top: 60px;
                }
            }
            /* 두 번째 사이트 아이템 - 첫 번째 위에 겹침 */
            &:nth-child(2) {
                background: var(--cardBg-color);
                background-size: cover;
                background-position: center;
                background-attachment: fixed;
                border: 1px solid rgba(255, 107, 107, 0.2);
                top: 90px; /* 20px씩 겹치게 */
                z-index: 3;
                position: relative;
                overflow: hidden;

                /* 프로젝트 정보 오버레이 */
                &::before {
                    content: '';
                    position: absolute;
                    top: 0;
                    left: 0;
                    right: 0;
                    bottom: 0;
                    background: linear-gradient(
                        135deg, 
                        rgba(67, 126, 235, 0.9) 0%, 
                        rgba(118, 75, 162, 0.8) 100%
                    );
                    z-index: 1;
                }
                
                /* 컨텐츠를 오버레이 위로 */
                .num, .text, .title, .btn, .info {
                    position: relative;
                    z-index: 2;
                }
                
                /* 두 번째 카드 특별 스타일링 */
                .text {
                    text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.5);
                    font-weight: 800;
                    
                    div {
                        background: rgba(255, 255, 255, 0.1);
                        backdrop-filter: blur(10px);
                        padding: 8px 16px;
                        margin: 4px 0;
                        border-radius: 8px;
                        border: 1px solid rgba(255, 255, 255, 0.2);
                    }
                }
                
                .title {
                    background: rgba(255, 255, 255, 0.95);
                    color: var(--black);
                    padding: 16px 20px;
                    border-radius: 12px;
                    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
                    backdrop-filter: blur(20px);
                    font-weight: 700;
                    text-align: center;
                }
                
                .btn a {
                    backdrop-filter: blur(10px);
                    box-shadow: 0 4px 16px rgba(0, 0, 0, 0.3);
                    
                    &:first-child {
                        background: rgba(255, 255, 255, 0.9);
                        color: var(--black);
                        border-color: rgba(255, 255, 255, 0.9);
                        
                        &:hover {
                            background: rgba(255, 255, 255, 1);
                            transform: translateY(-2px);
                        }
                    }
                    
                    &:last-child {
                        background: rgba(255, 255, 255, 0.1);
                        color: var(--white);
                        border-color: rgba(255, 255, 255, 0.3);
                        
                        &:hover {
                            background: rgba(255, 255, 255, 0.2);
                            transform: translateY(-2px);
                        }
                    }
                }
                
                .info {
                    background: rgba(0, 0, 0, 0.7);
                    backdrop-filter: blur(15px);
                    border: 1px solid rgba(255, 255, 255, 0.2);
                    
                    span {
                        color: var(--white);
                        font-weight: 500;
                        
                        &:first-child {
                            color: #ffd700;
                            font-weight: 600;
                        }
                    }
                }

                @media (max-width: 800px){ 
                    top: 80px;
                    background-attachment: scroll;
                }
            }
            /* 세 번째 사이트 아이템 - 두 번째 위에 겹침 */
            &:nth-child(3) {
                background: var(--cardBg-color);
                border: 1px solid rgba(78, 205, 196, 0.2);
                top: 110px; /* 20px씩 겹치게 */
                z-index: 2;

                @media (max-width: 800px){ 
                    top: 100px;
                }
            }
            /* 네 번째 사이트 아이템 - 세 번째 위에 겹침 */
            &:nth-child(4) {
                background: var(--cardBg-color);
                border: 1px solid rgba(255, 217, 61, 0.2);
                top: 130px; /* 20px씩 겹치게 */
                z-index: 1;

                @media (max-width: 800px){ 
                    top: 120px;
                }
            }
            /* 번호 스타일링 */
            .num {
                font-size: 4vw;
                line-height: 1;
                font-weight: 800;
                font-family: var(--mainNum-font);
                position: absolute;
                left: 20px;
                top: 20px;
                color: var(--text-muted);
                opacity: 0.3;
                transition: all 0.3s ease;

                @media (max-width: 800px) and (min-width: 481px) { 
                    font-size: 50px;
                    left: 16px;
                    top: 16px;
                }
                
                @media (max-width: 480px) { 
                    font-size: 40px;
                    left: 12px;
                    top: 12px;
                }
                
                @media (max-width: 320px) { 
                    font-size: 32px;
                    left: 10px;
                    top: 10px;
                }
            }
            
            &:hover .num {
                opacity: 0.6;
                transform: scale(1.1);
            }
            
            /* R&D 포털 카드 전용 스타일 */
            &.rd-portal {
                background-size: cover !important;
                background-position: center !important;
                background-attachment: fixed !important;
                
                @media (max-width: 800px) {
                    background-attachment: scroll !important;
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
                margin-bottom: 1.5rem;
                color: var(--text-primary);
                font-weight: 600;
                font-size: 1.5rem;
            }
            /* 버튼 스타일링 */
            .btn {
                display: flex;
                gap: 12px;
                margin-bottom: 1rem;
                
                /* 버튼 링크 */
                a {
                    padding: 8px 16px;
                    border-radius: 6px;
                    text-transform: uppercase;
                    font-size: 0.9rem;
                    font-weight: 500;
                    transition: all 0.3s ease;
                    border: 1px solid;
                    text-decoration: none;
                    
                    &:first-child {
                        background: var(--primary-color);
                        color: var(--black);
                        border-color: var(--primary-color);
                        
                        &:hover {
                            background: transparent;
                            color: var(--primary-color);
                        }
                    }
                    
                    &:last-child {
                        background: transparent;
                        color: var(--text-secondary);
                        border-color: var(--text-secondary);
                        
                        &:hover {
                            background: var(--text-secondary);
                            color: var(--black);
                        }
                    }
                }
            }
            /* 추가 정보 스타일링 */
            .info {
                position: absolute;
                left: 20px;
                bottom: 20px;
                right: 20px;
                background: rgba(0, 0, 0, 0.8);
                backdrop-filter: blur(10px);
                border-radius: 8px;
                padding: 12px 16px;
                border: 1px solid rgba(255, 255, 255, 0.1);
                display: flex;
                justify-content: space-between;

                @media (max-width: 800px){ 
                    flex-direction: column;
                    left: 16px;
                    right: 16px;
                    padding: 10px 12px;
                }

                /* 정보 항목 */
                span {
                    font-family: var(--mainEng-font);
                    font-size: 0.75rem;
                    color: var(--text-secondary);
                    font-weight: 400;
                    
                    &:first-child {
                        color: var(--primary-color);
                        font-weight: 500;
                    }
                    
                    @media (max-width: 800px) {
                        margin-bottom: 4px;
                        font-size: 0.7rem;
                    }
                }
            }
        }
    }
}
</style>