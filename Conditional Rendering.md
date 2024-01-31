# Conditional Rendering

- v-if / v-else

  ```
  <button @click="awesome = !awesome">전환</button>
  <h1 v-if="awesome">Vue는 정말 멋지죠!</h1>
  <h1 v-else>아닌가요? 😢</h1>
  ```

  v-if / v-else / v-else-if 를 사용할 때는 바로 다음에 오도록 한다.

- `<template>` 에서 v-if
  `<template>`에서 v-if를 사용함으로써 둘 이상에 요소를 조건부 렌더링을 할 수 있다. 이 때, `<template>`은 래퍼 역할을 하며 렌더링 될 때에는 표시되지 않는다.

  ```
  <template v-if="ok">
    <h1>제목</h1>
    <p>단락 1</p>
    <p>단락 2</p>
  </template>
  ```

- v-show

  if와 비슷하며 차이점은 v-show가 있는 엘리먼트는 항상 렌더링되고 DOM에 남아 있다. v-show는 엘리먼트의 display CSS 속성만 전환한다.
  `<template>` 와 v-else를 함께 사용할 수 없다.

- 일반적으로 v-if는 전환 비용이 더 높고, v-show는 초기 렌더링 비용이 더 높다. 따라서, 매우 자주 전환해야 하는 경우 v-show를, 실행 중에 조건이 변경되지 않는 경우 v-if를 사용하는 것이 좋습니다.

  - 요소 활성화 = v-show
  - data에 따른 조건 렌더링 = v-if
