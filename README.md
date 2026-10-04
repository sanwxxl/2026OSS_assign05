# Week 5 - Simple CRUD Service

## Deployment

- Vercel URL: 2026ossassign05-3y7xp05jz-sanwxxl.vercel.app

## Key Learning

1. JavaScript Array를 데이터베이스처럼 사용하여 데이터를 저장하고 관리하는 방법
2. render() 함수로 Array의 데이터를 DOM(Table)에 출력하는 방법
3. CRUD 구현하는 방법

## CRUD Service

### 주제
게임 관리 서비스

### 데이터 Field
| Field | 설명 | 타입 |
|---|---|---|
| id | 게임 고유 번호 | Number |
| name | 게임 이름 | String |
| company | 제작사 | String |
| price | 가격(원) | Number |
| playtime | 플레이타임(시간) | Number |

### 구현 방법
- **Create**: Form 입력값을 읽어 객체를 만들고 `push()`로 배열에 추가한 뒤 `render()`
- **Read**: `render()`에서 `forEach()`로 배열을 돌며 `<tr>`을 만들어 `tbody`에 출력
- **Update**: [수정] 클릭 시 `find()`로 게임을 찾아 Form에 표시하고, `editingId`로 수정 모드를 기억. [저장] 시 찾은 객체의 값을 변경
- **Delete**: `confirm()`으로 확인 후 `filter()`로 해당 id를 제외한 새 배열을 만들어 저장

## JavaScript

| 기능 | 사용한 곳 / 역할 |
|---|---|
| `getElementById()` | id로 HTML 요소(form, 입력칸, 버튼, tbody)를 찾아 변수에 저장 |
| `addEventListener()` | [추가/저장] 버튼에 click 이벤트를 연결해 클릭 시 추가 또는 수정 실행 |
| `innerHTML` | render()에서 tbody를 비우고, 게임마다 `<tr>` HTML 문자열을 넣어 표를 그림 |
| `forEach()` | render()에서 games 배열의 게임을 하나씩 꺼내 표의 한 줄로 만듦 |
| `push()` | Create: 입력값으로 만든 새 게임 객체를 배열 맨 뒤에 추가 |
| `find()` | Update: id가 같은 게임 하나를 찾아 Form에 값을 채우고, 저장 시 그 객체의 값을 변경 |
| `filter()` | Delete: 삭제할 id와 다른 게임만 남긴 새 배열을 만들어 games에 다시 저장 |
| `confirm()` | Delete: 삭제 전 확인/취소 창을 띄우고, 확인(true)일 때만 삭제 |
| `reportValidity()` | 버튼 클릭 시 form의 required, min, maxlength를 검사하고 틀리면 안내 후 중단 |
| `trim()` | 입력값 앞뒤 공백을 제거해 공백만 입력한 경우를 빈칸으로 처리 |
| `Number()` | 문자열인 입력값(.value)을 숫자로 변환해 price, playtime에 저장 |
| `textContent` | 수정 모드일 때 버튼 글자를 "저장", 끝나면 "추가"로 변경 |
| `render()` | 직접 만든 함수. 배열 내용을 표에 출력하며 시작, 추가, 수정, 삭제 후마다 호출 |

## AI / Search Usage

- 사용한 도구: Claude
- 사용 목적: 단계별 코딩 디버깅 용도로 사용, 및 가이드 역할 요청, 오류 원인 찾기 용도로 사용함.
- 적용 방법: 직접 짠 코드를 AI에게 보여주고, 점수를 메겨달라하면서 평가받음, 추가로 수정해야할 부분이나, develop할 부분을 claude가 짚어주면 그 부분 이해하면서 코드 수정 및 develop 진행.
- 새롭게 이해한 내용: validation할 때 required 같은 HTML Validation은 form이 제출(submit)될 때 브라우저가 검사하기 때문에, 새로고침을 막으려고 버튼을 type= button으로 바꿨던 것이 문제가되어 제출이 안 일어나니까 검사도 안 일어났었다. 그래서 그 부분을 해결하기 위해, reportVaidity() 함수를 알게되었고 제출 없이도 직접 검사하게끔 만들 수 있었다.

## Problem & Solution

| 문제 | 원인 | 해결 |
|---|---|---|
| 삭제 버튼이 표에 나오지 않음 | 문자열 연결 중 `+`가 빠져 문장이 끊김 | 줄 끝에 `+` 추가 |
| 버튼에 `game.name`을 넘기면 클릭해도 동작 안 함 | 따옴표 없는 문자열을 변수로 인식해 에러 | 고유값인 `id`를 넘기도록 변경 |
| 삭제 후 추가하면 id가 겹칠 수 있음 | `nextId`를 클릭할 때마다 새로 계산 | 함수 밖에서 한 번만 계산하고 `nextId++` |
| `required`가 동작하지 않음 | 버튼이 `type="button"`이라 form 제출이 일어나지 않음 | `reportValidity()`로 직접 검사 |
| 수정 중인 게임을 삭제하면 저장 시 에러 | `find()` 결과가 `undefined` | 삭제할 때 수정 모드 초기화 |

## Reflection

직접 코딩을 해보면서, function에 대한 감각을 더 익힐 수 있었고, CRUD 기능을 구현하는 것을 더 연습해야겠다고 느꼈다. 한 페이지에 CRUD를 구현하다보니, 저번 과제처럼 다시 클래스를 구분해서 개발해보고 싶다. 연습이 많이 필요하다고 느꼈다.