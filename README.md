# README

## 구현 과정

* Vue CLI 개발 환경
* 컴포넌트 기반 구조
* Vue Router



* 회원 관련 기능
  * 회원가입
  * 로그인
    * 로그인은 토큰 기반 인증 진행, 쿠키에 저장하여 활용
* 커뮤니티(게시판) 기능
  * 게시글 생성
  * 게시글 조회(목록, 상세보기는 구현X)



## 문제점

1. movie_api에서 CORS 설정을 완벽히 하지 않아서 로그인 등 요청을 했을 때 거부당했습니다.

   -> `CORS_ORIGIN_ALLOW_ALL = True` 를 settings.py에 추가



2. ListView.vue 에서 글쓰기 버튼을 누르면 CreateView.vue를 보여주는 과정 구현을 a 태그로 진행했습니다. 하지만 게시판 글쓰기 화면이 잠깐 비춰지고 바로 목록 페이지로 이동했습니다.

   ```vue
   <button @click="create">글쓰기</button>
   
   methods: {
           create() {
             this.$router.push({ name: 'Create' })
           },
   ```

   -> a 태그 대신 함수 create를 만들어 처리



## 페어프로그래밍 느낀점

다음날부터 진행될 최종 프로젝트를 페어와 같이 무사히 마쳤으면 하는 마음입니다.