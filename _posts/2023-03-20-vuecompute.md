---
layout: single
title: "📝 Vue.js Computed?"
toc: true
toc_sticky: true
toc_label: "Vue의 Computed"
categories: js
excerpt: "왜 있는걸까?"
tag: [js]
---

# 01. 왜 사용할까?

- template 내의 표현식은 매우 편리하지만, 간단한 표현식을 위한 것임
- 너무 많은 logic을 넣으면 유지관리가 어려울 수 도 있음

```js
export default {
  data() {
    return {
      author: {
        name: "John Doe",
        books: [
          "Vue 2 - Advanced Guide",
          "Vue 3 - Basic Guide",
          "Vue 4 - The Mystery",
        ],
      },
    };
  },
};
```

그리고 이상태에서 `author`가 이미 책을 가지고 있는지에 따라 msg를 표현하고 싶다면

```js
<template>
  <p>책을 가지고 있다:</p>
  <span>{{ author.books.length > 0 ? 'Yes' : 'No' }}</span>
</template>
```

- 벌써 template가 복잡해지는것이 느껴짐
- 하지만 더 큰 문제는 반응형 결과가 `author.books`에 의해 계산된다는 점 보다, template 내부에서 코드가 반복되었을 경우임
- 따라서 반응형 데이터를 표함한 복잡한 logic의 경우, `computed` 를 사용하는게 좋음

<br> 개선된 경우

```js
export default {
  data() {
    return {
      author: {
        name: "John Doe",
        books: [
          "Vue 2 - Advanced Guide",
          "Vue 3 - Basic Guide",
          "Vue 4 - The Mystery",
        ],
      },
    };
  },
  computed: {
    // 계산된 값을 반환하는 속성
    publishedBooksMessage() {
      // `this`는 컴포넌트 인스턴스를 가리킵니다.
      return this.author.books.length > 0 ? "Yes" : "No";
    },
  },
};
```

```js
<p>책을 가지고 있다:</p>
<span>{{ publishedBooksMessage }}</span>
```

- computed로 `publishedBookMessage`를 선언함
- `data`에 있는 `books` 배열의 값을 변경하면, 그에다라 `publishedBookMessage`가 바뀜

- 일반 속성처럼 template의 `computed`에 데이터를 바인딩할 수 있음
- Vue는 `publishedBooksMessage`의 값이 `author.books`에 의존한다는 것을 알고 있으므로, `author.books`가 변경되면 `publishedBooksMessage`를 바인딩해 의존하는 모든 것을 업데이트함

---

# 02. computed vs method

- `methods`를 사용해서 동일한 결과를 얻을 수 있음

```js
<template>
  <p>{{ calculateBooksMessage() }}</p>
</template>
```

```js
// 컴포넌트 내에서
methods: {
  calculateBooksMessage() {
    return this.author.books.length > 0 ? 'Yes' : 'No'
  }
}
```

- `computed`대신 `methods`를 사용해서 동일한 기능을 구현하고 정의할 수 있음
- 결과적으로 두 접근 방식은 실질적으로 완전히 동일함
- **그러나 `computed`는 의존하는 반응형을 기반으로 caching 한다는 것임**

> computed 속성은 의존한 반응형 중 일부가 변경된 경우에만 다시 평가됨 <br>
> 즉, `author.books`가 변경되지 않는 한, 여러곳에서 `publishedBooksMessage`를 접근한다면,<br> getter 함수를 다시 실행시키지 않고
> 이전에 계산된 결과를 즉시 반환함

- 따라서 Date.now()가 반응형으로써 의존된 것이 아니기 때문에 이후 계산된 속성이 업데이트되지 않음

```js
computed: {
  now() {
    return Date.now()
  }
}
```

**하지만 반대로 메서드 호출은 리렌더링이 발생할 때마다 항상 함수를 실행**

### **왜 케싱이 필요할까?**

> 캐싱이 필요한 이유는 무엇일까?
>
> 1. 거대한 배열을 루프 하며 많은 계산을 해야 하는 값비싼 비용의 list 속성이 있다고 가정해보자.
> 2. 그리고 list에 의존하는 또 다른 계산된 속성이 있을 수 있음
> 3. 캐싱이 없다면 우리는 list의 getter를 불필요하게 많이 실행할 것임!
> 4. 캐싱을 원하지 않는 경우에만 메서드 호출을 사용하면됨

---

# 03. 그러면 언제 사용해야 할까?

- 이름 그대로 `computed` 이므로 read only라는것을 명심하고 사용해야 함
- 비동기 요청을 하거나, DOM을 변경하면 절대 안됨! -> side effect가 나타나면 안댐
- 하고싶으면 watch를 사용해야함

다음 포스팅은 watch가 될듯
