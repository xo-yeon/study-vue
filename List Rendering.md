# Conditional Rendering

- v-for
  for(param in obj) 과 items.map((item) => item) 처럼 배열속 각 요소를 렌더링 할 수 있게 한다.

  ```
  const items = ref([{ message: 'Foo' }, { message: 'Bar' }])

  <li v-for="item in items">
    {{ item.message }}
  </li>

  // 인덱스도 사용가능
  <li v-for="(item, index) in items">
    {{ index }} - {{ item.message }}
  </li>

  //구조 분해 사용가능
  <li v-for="({ message }, index) in items">
    {{ message }} {{ index }}
  </li>
  ```

- 객체에 v-for 사용하기
  object.keys()의 결과와 같음

  ```
  const myObject = reactive({
    title: 'Vue에서 목록을 작성하는 방법',
    author: '홍길동',
    publishedAt: '2016-04-10'
  })

  // obj에 value, key index 모두 사용 가능
  <li v-for="(value, key, index) in myObject">
    {{ index }}. {{ key }}: {{ value }}
  </li>
  ```

- 숫자 범위에 v-for 사용
  v-for는 정수를 사용할 수도 있다. 이 경우 1...n 범위를 기준으로 템플릿을 여러 번 반복.

  ```
  // n은 0이 아니라 1부터 시작
  <span v-for="n in 10">{{ n }}</span>
  ```

- v-if와 동일하게 `<template>`에서 v-for 사용가능

- v-if가 v-for보다 우선순위가 높기 때문에 v-if 조건문에서 v-for 변수에 접근할 수 없다.

- key

  ```
  DOM Node의 위치가 변경되면 DOM Tree구조가 변경 되었기 때문에 Render Tree를 재구성한후에, 재 구성된 Node들의 위치,크기,깊이등을 다시 계산하는 Reflow 과정을 수행하고, DOM Node를 다시 그려 내는 Repaint 과정을 거치게 됩니다. 만약 Node를 이동하지 않고 Node 내부의 컨텐츠만 변경한다면, 렌더 트리 재구성이나 Reflow를 생략하고 해당 Node를 Repaint하기 때문에 효율적입니다.

  만약 자식 컴포넌트가 상태를 가진다면(예를 들어, Input 폼에 사용자가 값을 입력 해두었다면, 그 입력값을 지우면 안되기 때문에) 해당 자식 컴포넌트를 재사용 할 수 없기 때문에, 이렇게 기존 DOM Node를 재사용하는 방법은 유효한 방법이 아닐 것 입니다.
  ```

  `<template v-for>`를 사용할 때 key는 `<template>` 컨테이너에 있어야 한다.

  ```
  <template v-for="todo in todos" :key="todo.name">
    <li>{{ todo.name }}</li>
  </template>
  ```

- 컴포넌트 v-for 사용
  v-for으로 컴포넌트로 데이터를 전달하게 되면, props와 v-for에 사용하는 범위가 애매해지기 때문에 v-for 적용 후 props로도 데이터를 전달해야한다.

  ```
    <MyComponent
    v-for="(item, index) in items" //각 아이템을 사용하도록 하고
    :item="item" //props로 아이템 전달
    :index="index"
    :key="item.id"
  />
  ```

- 수정 메서드
  데이터를 업데이트 시킴

  ```
  push()
  pop()
  shift()
  unshift()
  splice()
  sort()
  reverse()
  ```

- 배열 교체
  수정 메서드와 달리 새 배열을 리턴시키기 때문에 ref에 다시 적용해야함

  ```
  // `items`는 값이 있는 배열의 ref라고 가정된 경우입니다.
  items.value = items.value.filter((item) => item.message.match(/Foo/))
  ```

- 필터링/정렬 결과 표시

  원본 데이터를 실제로 수정하거나 교체하지 않고 필터링되거나 정렬된 결과를 표시하로 싶을 때 함수를 통해 리턴하여 보여준다.
  ex) 패치 해온 데이터 리스트 필터 및 정렬

  ```
  const numbers = ref([1, 2, 3, 4, 5])

  const evenNumbers = computed(() => {
    return numbers.value.filter((n) => n % 2 === 0)
  })

  <li v-for="n in evenNumbers">{{ n }}</li>
  ```

- 중첩된 v-for 루프 내부에서 사용

  ```
  const sets = ref([
    [1, 2, 3, 4, 5],
    [6, 7, 8, 9, 10]
  ])

  function even(numbers) {
    return numbers.filter((number) => number % 2 === 0)
  }

  <ul v-for="numbers in sets">
    <li v-for="n in even(numbers)">{{ n }}</li>
  </ul>
  ```

- reverse / sort >> 이 부분 나중에 다시 확인

  계산된 속성에서 reverse()와 sort() 사용에 주의! 이 두 가지 방법은 원본 배열을 수정하므로 계산된 속성의 getter 함수에서 피해야한다. 다음 메서드를 호출하기 전에 원본 배열의 복사본을 만든다.

  ```
  - return numbers.reverse()
  + return [...numbers].reverse()
  ```
