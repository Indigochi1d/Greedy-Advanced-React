# 02-3. 전역상태관리 - Redux

## 🎯 요구사항
- Redux toolkit를 사용해서 애플리케이션 내의 Recoil로부터의 마이그레이션을 해보세요.
  ```shell
  npm install redux react-redux @reduxjs/toolkit
  ```
- props에 대한 요구사항은 2-1 요구사항과 같습니다.
- Redux를 **왜** 사용하는지, Recoil과 비교했을때 어떤 점이 달랐는지, 또 trade-off가 있는지 적어주세요.
  - 기술적인 것도 좋고 개발자의 경험 측면에서도 좋습니다.
- Redux-Actions을 사용하세요.
  ```shell
  npm add redux-actions
  ```
### 😗구현 예시
- 컴포넌트의 이름이나 구조는 마음대로 변경해도 좋습니다.
```javascript
import { createStore } from 'redux'

/**
 * 이것이 (state, action) => state 형태의 순수 함수인 리듀서입니다.
 * 리듀서는 액션이 어떻게 상태를 다음 상태로 변경하는지 서술합니다.
 *
 * 상태의 모양은 당신 마음대로입니다: 기본형(primitive)일수도, 배열일수도, 객체일수도,
 * 심지어 Immutable.js 자료구조일수도 있습니다.  오직 중요한 점은 상태 객체를 변경해서는 안되며,
 * 상태가 바뀐다면 새로운 객체를 반환해야 한다는 것입니다.
 *
 * 이 예제에서 우리는 `switch` 구문과 문자열을 썼지만,
 * 여러분의 프로젝트에 맞게
 * (함수 맵 같은) 다른 컨벤션을 따르셔도 좋습니다.
 */
function counter(state = 0, action) {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1
    case 'DECREMENT':
      return state - 1
    default:
      return state
  }
}

// 앱의 상태를 보관하는 Redux 저장소를 만듭니다.
// API로는 { subscribe, dispatch, getState }가 있습니다.
let store = createStore(counter)

// subscribe()를 이용해 상태 변화에 따라 UI가 변경되게 할 수 있습니다.
// 보통은 subscribe()를 직접 사용하기보다는 뷰 바인딩 라이브러리(예를 들어 React Redux)를 사용합니다.
// 하지만 현재 상태를 localStorage에 영속적으로 저장할 때도 편리합니다.

store.subscribe(() => console.log(store.getState())))

// 내부 상태를 변경하는 유일한 방법은 액션을 보내는 것뿐입니다.
// 액션은 직렬화할수도, 로깅할수도, 저장할수도 있으며 나중에 재실행할수도 있습니다.
store.dispatch({ type: 'INCREMENT' })
// 1
store.dispatch({ type: 'INCREMENT' })
// 2
store.dispatch({ type: 'DECREMENT' })
// 1
```


## ✅ 키워드
- props drilling
- 전역상태관리
  - Redux
  - store
  - Reducer
  - dispatch
  - useReducer
  - useDispatch

## 🧙‍♀️ 진행 가이드
- 진행시간 : 2시간 내에 완료하는 것을 목표로 합니다.

## 🔗 참고 문서
- [Redux 공식문서](https://ko.redux.js.org/introduction/getting-started/)
- [테코톡(에프이의 useReducer)](https://www.youtube.com/watch?v=xnlCNIpzQq0&list=PLgXGHBqgT2TvpJ_p9L_yZKPifgdBOzdVH&index=42)