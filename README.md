# node-bird(~ing)
## next.js 역활
### 전통적인 방법
- 프론트 서버에서 백엔트 서버의 데이터를 받구 프론트에서 데이터를 가지구 화면과 함께 브라우저에게 전달
- 한번에 화면을 그려주지만 단점은 화면 그려주는 시간이 길어진다.
### 리액트 뷰 등 싱글페이지애플리케이션
- 데이터 없이 화면만 받구(프론트에서) 백엔드에서 직접 데이터를 받는다 브라우저에서
- 화면을 먼저 그려주고 로딩창을 띄어서 그동안 백엔드에서 데이터를 받아서 그려준다
- 앞으로 바뀔거에 대한 화면까지 받아오기 때문에 시간이 더 걸릴수 잇지만 먼저 화면에 그려주기때문에 
사용자 입장에선 더 좋을수도! 사용자가 빠르게 인터랙션이 필요할때 주로 사용
### 서버사이드 랜더링 :  검색을 위해서
1. 프리랜더 :  검색엔진이라구 미리 파악해서 구분해서 보내준다
2. 서버사이드 랜더링 : 첫방문만 전통적인 방식으로 하구 그다음 페이지 전환일때는 리액트 방식이으로
<br> 하이브리드 방식
=> 어드민페이지를 사용할때는 검색 엔진에 노출 안되두 되기에 굳이 서버사이드 렌더링 방식을 안해두 된다

### next.js의 특징
1. 넥스트는 라우팅을 알아서 해준다
- 동적 라이팅 기능이 추가되었다.

## 준비사항
1. 넥스트 설치
> npm init 
> npm i next@9 // 버젼은 @로 
<Br>

    "scripts": {
        "dev": "next"
      },
      
<br>
> npm i react react-dom

2. ant디자인 설치
> npm i antd styled-components @ant-design/icons
3. eslint : 코드 규칙<br>
D는 개발모드
> npm i eslint -D 
<br>
> npm i eslint-plugin-import -D
<bt>
> npm i eslint-plugin-react -D
<Br>
> npm i eslint-plugin-react-hooks -D

<br>
설치 후  .eslintrc 파일을 만들어주고 해당 규칙을 기재해준다 <br>
그리고 eslint의 대한 에디터 설정두 해준다

### 알게 된점
1. target='_blank' 시 보안에 취약하기 때문에 함께 rel='noreferrer noopener' 사용
2. 컴포넌트의 props로 넘겨주는 함수는 useCallback을 써주기 => 최적화를 위해
3. 반복되는 패턴은 커스텀 훅으로 처리
4. 객체형식의 스타일을 인라인으로 주면 객체는 서로 다른 거라 인식하기 때문에 가삼돔이 한번더 리렌더링 된다 => 데이터가 변한 부분도 아닌데 객체가 서로 다른거라 인식하기 때문
<br>=> 스타일드 컴포넌트로 변환! or useMemo
<br>
useMemo와 useCallback 의 차이점
값을 캐싱 : 함수를 캐싱
5. 함수형 컴포넌트 리랜더링 :  함수부분이 리렌더링 되는데 이전 컴포넌트와 현재컴포넌트를 비교해서 바꾼 부분만 리렌더링
6. 컴포넌트를 나누는 기준 : props 갯수가 많아지면 구분해서 컴포넌트를 나눠두 된다 

## 유용한 것
### 커스텀훅
1. 중복되는 부분을 커스텀 훅으로 빼준다.
2. 리턴되는 부분을 주의하라!

### 이미지 캐루셀

### saga
1. yield 중단점
2. all 함수를 함쳐준다
3. 사가의 함수는 function 키워드 앞에 *를 붙여준다.
4. throttle : 입력 시간 후에 요청을 받는다.
5. takeLatest : 요청 2번이상 간 경우 맨 서버에서 마지막의 요청만 받는다
6. put: 디스패치와 같은 역활
ex)
```$xslt
    function* loadPosts(action) {
      try {
        // const result = yield call(loadPostsAPI, action.data);
        yield delay(1000);
        yield put({
          type: LOAD_POSTS_SUCCESS,
          data: generateDummyPost(10),
        });
      } catch (err) {
        console.error(err);
        yield put({
          type: LOAD_POSTS_FAILURE,
          data: err.response.data,
        });
      }
    }
```
7. call : api 연동할때 쓰인다  
ex)
```$xslt
// const result = yield call(loadPostsAPI, action.data);

function loadPostsAPI(data) {
  return axios.get('/api/posts', data);
}
```
### 해시태크 링크 연결 (정규식 사용)
- 해시태그 찾는 정규표현식 => /(#[^\s#]+)/g)
- g 글로버
- . 한글자
- .. 두글자
- +모든글자
- [] 여기 안아ㅔ 적은것들중에 선택
- [^여기안에 들어간 것은 제외]
- \s 공백
- \#[^\s#]+/g =># 뒤에 잇는 글자 공백과 다음 #전까지 찾는 정규표현
### immer
> import produce from '../util/produce';
- 알아서 불변성을 지켜준다
1. draft은 리듀서 안에서 쓰는데 state(리듀서 안에서의) 역활을 한다.
### faker
1. 가상 더미 데이터 

### 인피니트 스크롤 (리액트 적용)

### 리덕스 툴킷

### shotID
> import shortId from 'shortid';  
1. 곂치치 않도록 알아서 id 값을 부여


