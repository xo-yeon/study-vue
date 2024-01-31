# Reactivity Fundamentals

- ref

  상태가 변하는 값은 ref를 통해 선언
  객체로 저장을 해도 깊은 비교가 가능하다.

  ref가 변경되면 dom은 자동으로 업데이트 된다.
  여러번 상태 변경을 실행하던 컴포넌트는 한 번만 업데이트한다.
  업데이트 완료 후 다른 작업을 실행하고 싶을 때는 nextTick()을 사용한다.

  ```
  import { ref, nextTick } from 'vue'

  const count = ref(0)

  // html문에서도 사용 가능
  <button @click="count++">
    {{ count }}
  </button>


  // nextTick()
  async function increment() {
    count.value++
    await nextTick()
  // 이제 DOM이 업데이트되었습니다.
  }

  ```

- setup
  ref에 접근하기 위해서는 setup에서 사용되어야 하며,
  sfc(single file components)를 사용하면 해당 문법을 간단하게 표현할 수 있다.

  ```
  <script setup>
      ...
  </script>
  ```

- reactive() 🏹 재 정독 필요

  상태를 저장하여 변경할 수 있는 또 다른 api

  ```
  import { reactive } from 'vue'

  const state = reactive({ count: 0 })
  ```
