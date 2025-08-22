<!-- /src/components/IntroSection.vue -->
<script setup>
// 불러오는 데이터 관련 설명
// 별칭(@)을 안 쓰면 아래 줄을 이렇게 바꾸세요: import { introText } from "../constants";
import { introText } from "@/constants";
import { ref } from 'vue';

// 이미지 처리 관련 설명
// 이미지도 번들러 추적을 위해 import 후 바인딩 권장
// 별칭 안 쓰면 "../assets/img/about.jpg"
import aboutImg from "@/assets/img/about.jpg";

// 호버 상태를 관리하는 변수
const isHover = ref(false);

// 마우스 오버 이벤트 핸들러
const handleMouseEnter = () => {
  isHover.value = true;
};

// 마우스 아웃 이벤트 핸들러
const handleMouseLeave = () => {
  isHover.value = false;
};
</script>

<template>
  <!-- 소개 섹션: 자기소개와 프로필 이미지를 포함하는 영역 -->
  <section id="intro">
    <!-- 소개 섹션 내부 컨테이너 -->
    <div class="intro__inner">
      <!-- 소개 섹션 제목 -->
      <h2 class="intro__title">{{ introText.title }}</h2>

      <!-- 장식용 라인 요소들 (스크린리더에서는 읽히지 않음) -->
      <div class="intro__lines" aria-hidden="true">
        <span class="line"></span><span class="line"></span><span class="line"></span>
        <span class="line"></span><span class="line"></span><span class="line"></span>
        <span class="line"></span>
      </div>

      <!-- 소개 텍스트와 이미지 영역 -->
      <div class="intro__text" @mouseenter="handleMouseEnter" @mouseleave="handleMouseLeave">
        <!-- 소개 텍스트 -->
        <div class="text" v-if="!isHover">
          <div>{{ introText.desc[0] }}</div>
          <div>{{ introText.desc[1] }}</div>
          <div>{{ introText.desc[2] }}</div>
        </div>
        <div class="textcontent" v-else>
          <div class="contact-item">
            <span class="contact-label">Email</span>
            <span class="contact-value">lhg2196@naver.com</span>
          </div>
          <div class="contact-item">
            <span class="contact-label">Phone</span>
            <span class="contact-value">010-8466-2196</span>
          </div>
        </div>
        <!-- 프로필 이미지 -->
        <div class="img">
          <img :src="aboutImg" alt="어바웃" />
        </div>
      </div>

      <!-- 하단 장식용 라인 -->
      <div class="intro__lines bottom" aria-hidden="true">
        <span class="line"></span><span class="line"></span><span class="line"></span>
        <span class="line"></span><span class="line"></span><span class="line"></span>
        <span class="line"></span>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
/* 소개 섹션 기본 스타일링 */
#intro { height: 100vh; /* 화면 전체 높이로 설정 */ }
/* 소개 섹션 내부 컨테이너 스타일링 */
.intro__inner {
  width: 100%; height: 100%; /* 부모 요소 차지 */
  display: flex; align-items: flex-start; justify-content: flex-end; /* 하단 정렬 */
  flex-direction: column; padding: 16px; /* 세로 배치와 여백 */
  overflow-x: hidden; /* 가로 스크롤 방지 */
  max-width: 100vw; /* 뷰포트 너비 초과 방지 */

  /* 모바일 화면에서의 정렬 조정 */
  @media (max-width: 800px){ 
    justify-content: center; /* 모바일에서는 가운데 정렬 */
    padding: 12px; /* 모바일에서 패딩 축소 */
  }

  /* 소개 섹션 제목 스타일링 */
  .intro__title {
    font-size: 10vw; text-transform: uppercase; line-height: 1; font-weight: 800; /* 크고 굵게 */
    white-space: nowrap; text-indent: -0.5vw; letter-spacing: -0.3vw; /* 줄바꿈 방지와 글자 간격 조정 */
    /* 아주 작은 화면에서는 제목 숨김 */
    @media (max-width: 320px){ display: none; }
  }

  /* 소개 텍스트 영역 스타일링 */
  .intro__text {
    width: 100%; height: 40vh; background-color: var(--black); color: var(--white); /* 배경과 글자색 */
    display: flex; align-items: center; justify-content: space-between; /* 양쪽 정렬로 변경 */
    position: relative; /* 내부 요소 배치를 위한 기준점 */
    overflow: hidden; /* 넘치는 부분 숨김 */
    padding: 0 2rem; /* 좌우 여백 추가 */

    /* 모바일에서는 세로 배치 */
    @media (max-width: 800px) {
      flex-direction: column;
      justify-content: center;
      padding: 1rem;
    }

    /* 텍스트 스타일링 */
    .text {
      font-size: 3vw; line-height: 1; font-weight: 900; text-transform: uppercase; /* 크고 굵게, 대문자로 */
      text-decoration: underline; text-align: center; position: relative; z-index: 100; /* 밑줄과 중앙 정렬 */
      transition: all 0.3s; cursor: all-scroll; /* 호버 효과와 커서 스타일 */
      flex: 1; /* 남은 공간 차지 */
      max-width: 60%; /* 최대 너비 제한 */

      /* 태블릿에서 크기 조정 */
      @media (max-width: 800px) and (min-width: 481px) { 
        font-size: 28px;
        max-width: 100%;
        margin-bottom: 1rem;
      }

      /* 모바일에서는 고정 크기로 설정 */
      @media (max-width: 480px){ 
        font-size: 22px;
        max-width: 100%;
        margin-bottom: 1rem;
      }
      
      @media (max-width: 320px) {
        font-size: 18px;
      }
    }
    
    /* 마우스 오버 시 나타나는 텍스트 스타일링 */
    .textcontent {
      font-size: 1.5vw; /* 기본 폰트 크기의 약 60% */
      text-align: left; /* 왼쪽 정렬 */
      text-decoration: none; /* 밑줄 제거 */
      text-transform: none; /* 대문자 변환 제거 */
      font-weight: 900; /* 3배 더 두껍게 */
      line-height: 1.5; /* 줄간격 늘림 */
      flex: 1; /* 남은 공간 차지 */
      max-width: 60%; /* 최대 너비 제한 */
      display: flex;
      flex-direction: column;
      justify-content: center;
      
      .contact-item {
        margin-bottom: 1rem; /* 항목 간격 */
        display: flex;
        flex-direction: column;
        
        .contact-label {
          font-weight: 700;
          font-size: 1.2vw;
          margin-bottom: 0.2rem;
          opacity: 0.8;
        }
        
        .contact-value {
          font-weight: 900;
          letter-spacing: 0.05rem;
        }
      }
      
      /* 모바일에서는 고정 크기로 설정 */
      @media (max-width: 800px){ 
        font-size: 16px; /* 모바일에서는 조금 더 큰 크기로 설정 */
        max-width: 100%; /* 모바일에서는 전체 너비 사용 */
        text-align: center; /* 모바일에서는 중앙 정렬 */
        margin-bottom: 1rem;
        
        .contact-item {
          margin-bottom: 0.8rem;
          
          .contact-label {
            font-size: 14px;
          }
          
          .contact-value {
            font-size: 16px;
          }
        }
      }
    }

    /* 프로필 이미지 스타일링 */
    .img {
      width: 30vh; height: 30vh; border-radius: 25%; overflow: hidden; /* 원형 이미지 */
      flex-shrink: 0; /* 이미지 크기 고정 */
      margin-left: 2rem; /* 텍스트와의 간격 */
      transition: all 0.3s; /* 호버 효과 */

      /* 데스크톱에서 이미지 크기 조정 */
      @media (min-width: 1200px) {
        width: 35vh;
        height: 35vh;
      }

      /* 태블릿에서는 이미지 크기 조정 */
      @media (max-width: 800px) and (min-width: 481px) {
        width: 25vh; 
        height: 25vh;
        margin-left: 0;
        margin-top: 1rem;
      }
      
      /* 모바일에서는 이미지 크기 축소 */
      @media (max-width: 480px) {
        width: 20vh; 
        height: 20vh;
        margin-left: 0;
        margin-top: 1rem;
      }

      /* 작은 화면에서는 이미지 크기 더 축소 */
      @media (max-width: 320px){ 
        width: 15vh; 
        height: 15vh;
      }
      
      /* 이미지 요소 자체 스타일링 */
      img {
        width: 100%;
        height: 100%;
        object-fit: cover; /* 이미지 비율 유지하며 컨테이너에 맞춤 */
      }
    }

    /* 호버 효과: 이미지 스케일 변화 */
    &:hover .img { 
      transform: scale(1.05); /* 이미지 살짝 확대 */
      
      @media (max-width: 800px) {
        transform: scale(1.02); /* 모바일에서는 덜 확대 */
      }
    }
  }

  /* 장식용 라인 컨테이너 */
  .intro__lines {
    width: 100%; /* 전체 너비 차지 */

    /* 각 라인 스타일링 */
    .line {
      display: block; width: 100%; height: 1px; background-color: var(--black); /* 기본 라인 */
      margin-bottom: 0.5vw; /* 라인 간격 */

      /* 점점 두꿈져지는 라인 패턴 */
      &:nth-child(1){ height: 1px; /* 가장 얼음 */ }
      &:nth-child(2){ height: 2px; }
      &:nth-child(3){ height: 5px; }
      &:nth-child(4){ height: 9px; }
      &:nth-child(5){ height: 13px; }
      &:nth-child(6){ height: 17px; }
      &:nth-child(7){ height: 25px; /* 가장 두꿈 */ }
    }

    /* 하단 라인 특별 스타일 */
    &.bottom .line {
      margin-top: 0.5vw; margin-bottom: 0; display: none; /* 기본적으로 숨김 */
      /* 모바일에서는 표시 */
      @media (max-width: 800px){ display: block; }
      /* 상단과 반대 순서로 두께가 점점 얼어지는 패턴 */
      &:nth-child(1){ height: 25px; /* 가장 두꿈 */ }
      &:nth-child(2){ height: 17px; }
      &:nth-child(3){ height: 13px; }
      &:nth-child(4){ height: 9px; }
      &:nth-child(5){ height: 5px; }
      &:nth-child(6){ height: 2px; }
      &:nth-child(7){ height: 1px; /* 가장 얼음 */ }
    }
  }
}
</style>