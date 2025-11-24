# 📌 Travel Maker – 여행 기록 & 숙소 예약 통합 플랫폼

> **여행 계획부터 후기까지 한 번에 관리하는 올인원 여행 플랫폼**

Travel Maker는 여행 계획 작성부터 숙소 예약, 여행 후기 기록, 미니홈피 기반의 개인 기록 공간까지
**여행의 모든 과정을 하나의 서비스에서 해결할 수 있도록 설계된 웹 서비스**입니다.

> 거리두기 해제 이후 증가한 여행 수요를 반영하여
> 누구나 쉽고 즐겁게 여행 정보를 기록하고 공유할 수 있는 환경을 제공하는 것이 목표입니다.

---

## 📚 Contents

* [프로젝트 개요](#-프로젝트-개요)
* [주요 기능](#-주요-기능)
* [아키텍처 및 기술 스택](#-아키텍처-및-기술-스택)
* [DB 테이블 설계](#-db-테이블-설계)
* [핵심 기능 상세](#-핵심-기능-상세)
* [데이터 수집](#-데이터-수집)
* [Face Detection / Speech to Text / Chatbot](#-face-detection--speech-to-text--chatbot)
* [팀원 역할](#-팀원-역할)
* [프로젝트 회고](#-프로젝트-회고)

---

# 🌍 프로젝트 개요

Travel Maker는 여행 네비게이터 역할을 수행하는 플랫폼으로 다음의 기능을 제공합니다.

* 여행 계획 생성 & 일정 관리
* 여행 다이어리/사진 기록
* 미니홈피 기반의 개인 프로필 공간
* 숙소 리스트·상세 조회 및 예약 기능
* 실시간 리뷰, 별점, 검색 필터
* 챗봇, 음성인식, 얼굴 감정 분석 기능

---

# ✨ 주요 기능

## 1) 🧳 여행 기록 & 다이어리

* 날짜별 여행 기록 추가
* 일정/장소/사진 업로드
* Kakao Map API 기반 주소 검색
* 사진/썸네일 실시간 미리보기
* Ajax 기반 댓글 CRUD & 페이징 처리
* 여행 계획 캘린더(DateRangePicker) 적용

---

## 2) 🏠 미니홈피 시스템

* 프로필 이미지, 인사말 수정 (AJAX)
* 방문자 수 카운트 (쿠키 기반)
* 배경 음악 재생 (sessionStorage)
* 다이어리/사진첩 작성 및 삭제

---

## 3) 🏨 숙소 예약 기능

* 지역/유형/날짜/가격/별점 필터
* 호텔 썸네일·사진·객실·리뷰 연동
* Dynamic Query 기반의 복합 검색
* 호텔/객실 상세 페이지 구성

---

## 4) 👤 회원 시스템

* 회원가입 Toggle UI
* 아이디/이메일/닉네임 중복 체크 AJAX
* AOP 기반 로그인/로그아웃 로깅
* MyPage 정보 수정 (Trigger 기반 연동)

---

# 🏗 아키텍처 및 기술 스택

## ✔ Backend

* Java / Spring Boot
* Spring MVC / MyBatis
* Oracle DB
* AOP (로그 기록)
* REST API

## ✔ Frontend

* HTML / CSS / JavaScript / jQuery
* Thymeleaf
* Kakao Map API
* DateRangePicker

## ✔ Data

* Selenium 기반 크롤링

  * 트리플: 여행지 데이터
  * 야놀자: 호텔 데이터

## ✔ Machine Learning / AI

* CNN 기반 Face Detection (감정 분석)
* Speech-to-Text
* Kakao Chatbot API

---

# 🗃 DB 테이블 설계

<img width="764" height="587" alt="Image" src="https://github.com/user-attachments/assets/9f83688a-230c-4300-88c9-d42b60707f8a" />
<img width="1066" height="656" alt="Image" src="https://github.com/user-attachments/assets/a31a88df-4d56-4310-b08d-6e04ce9a5c2d" />
<img width="1812" height="968" alt="Image" src="https://github.com/user-attachments/assets/0d94bdca-37ba-43c6-8417-f3756a3c859f" />

### ▪ 회원/로그인 관련

* Member
* LoginLog (AOP)

### ▪ 여행 계획 & 기록

* RecDiary
* RecSchedule
* RecPhoto
* RecHashtag
* Equipment/EquipmentDetail

### ▪ 미니홈피

* MiniHome
* MiniDiary
* MiniPhoto

### ▪ 숙소 예약

* Hotel
* Room
* HotelPhoto
* Review

---

# 🔧 핵심 기능 상세

## ✔ 로그인/회원가입

* Toggle UI로 폼 전환
* AJAX 중복 체크
* e.preventDefault() 사용
* AOP 기반 로그인/로그아웃 기록 저장

## ✔ 여행 다이어리 입력

* 일차 추가 제한 (여행일자 초과 불가)
* 시간/장소 일정 추가
* Kakao 지도 검색 팝업 → 부모창 값 전달
* FileReader 기반 이미지 미리보기
* 여러 이미지 업로드 및 삭제 기능

## ✔ 여행 다이어리 댓글

* AJAX CRUD
* RestController로 데이터 전송
* 페이지네이션 적용

## ✔ 여행 계획 관리

* 행 추가/삭제(+/-)
* 순서 이동 기능
* Mapper에서 Insert All + sequence.nextVal
* @Transactional로 전체 처리 보장

## ✔ 숙소 검색 & 리스트

* 조건부 검색을 위한 Dynamic Query 활용
* 지역, 가격, 날짜, 별점 등 복합 조건 지원
* 호텔·객실·리뷰·사진 테이블 결합
* 최저가, 평균 평점 표시

---

# 📊 데이터 수집

### ▪ 트리플(여행지 정보)

* 여행지 리스트 → 상세 URL 추출
* 각 페이지에서 여행지 정보 스크래핑

### ▪ 야놀자(호텔 정보)

* 호텔 TOP 50 리스트 → 상세정보 추출
* 호텔명, 별점, 인사말, 기본정보 수집

### 사용 모듈

```
selenium
webdriver
tqdm
urlretrieve
os, time
```

수집한 CSV는 SQLDeveloper를 이용해 DB에 Import하여 사용.

---

# 🤖 Face Detection / Speech to Text / Chatbot

## ✔ Face Detection

* CNN 기반 감정 분류 모델
* softmax 다중 분류
* 이미지 정규화 후 학습
* 예측 결과 화면 표시

## ✔ Speech to Text

* 음성 업로드 후 텍스트 변환
* Django Views.py 기반

## ✔ Kakao Chatbot API

* 여행 추천/호텔 추천 기본 챗봇 구성

---

# 👥 팀원 역할

### **팀장 김지은**

* 프로젝트 총괄, 일정 관리
* 여행 기록/계획 UI & 기능
* DB 설계 & 구현
* FaceDetection, Kakao Map API

### **김우혁**

* 미니홈피 다이어리/사진첩
* 여행 일정 캘린더
* 게시판/로그인 공통 기능

### **김유리나**

* 호텔 예약 기능 핵심
* Transformer 기반 NLP
* 카카오 챗봇
* 데이터 설계

### **성대경**

* 마이페이지 & 회원수정
* 미니홈피 UI/DB
* 여행 커뮤니티 게시판

### **신민**

* 숙소 예약 및 검색
* Ajax 댓글 기능
* Speech To Text

### **윤정재**

* 전체 UI 디자인
* 호텔 상세/리뷰 페이지
* CSS & jQuery

### **이준희**

* 미니홈피, BGM, 방문자수
* DB 설계 및 다이어리 기능

---

# 📝 프로젝트 회고

* 협업과 소통의 중요성 체감
* 프로젝트 설계 초기의 중요성 학습
* 오류 해결 과정에서 개발 역량 성장
* 새 기술을 적용하며 자신감 향상
* 짧은 기간 동안 팀워크를 통해 성장
* 기술적 도전 및 성취감 경험
* 함께 이겨낸 시간들이 큰 힘이 됨

---

# 📸 Screenshots

<img width="1116" height="539" alt="Image" src="https://github.com/user-attachments/assets/86163555-ada6-4af5-bda5-df608f4f8ff1" />

---

# 🙏 감사합니다

프로젝트를 함께한 모든 팀원들의 노력으로 완성된 여행 플랫폼 Travel Maker.
앞으로도 기술적 성장과 협업을 통해 더 나은 서비스를 만들고자 합니다.

