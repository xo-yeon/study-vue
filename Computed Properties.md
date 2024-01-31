# Computed Properties

- computed

  값을 가져오기 전 계산이 필요할 때 사용
  vue에서는 상수로 선언하여 가져올 수 없다.
  상태값이 변경됨에 따라 계산된 값도 업데이트되어 가져오려면 computed를 사용해야한다.

  ```
  <script setup>
  import { reactive, computed } from 'vue'

  const author = reactive({
    name: 'John Doe',
    books: [
      'Vue 2 - Advanced Guide',
      'Vue 3 - Basic Guide',
      'Vue 4 - The Mystery'
    ]
  })

  // 계산된 ref
  const publishedBooksMessage = computed(() => {
    return author.books.length > 0 ? 'Yes' : 'No'
  })
  </script>

  <template>
    <p>책을 가지고 있다:</p>
    <span>{{ publishedBooksMessage }}</span>
  </template>
  ```
