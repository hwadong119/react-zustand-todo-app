## zustand 설치

```terminal
npm install zustand
```

<br><br>

## store 생성

- store 생성 후 안에 원하는 값과 그 값을 업데이트 해주는 함수를 넣음

- store는 hooks로 되어있음

- store를 생성할 때 create 메서드를 사용하여 선언

- set 함수는 상태를 변경

```javascript
import { create } from "zustand";

export const useCounterStore = create((set) => ({
  count: 1,
  increment: () => set((state) => ({ count: state.count + 1}))
}))
```

<br><br>

## persist middleware를 이용하여 저장소의 데이터 유지하기

persist()에 감싸주기만 하면 됨

```javascript

import { create } from "zustand";
import { persist } from 'zustand/middleware'

export const useCounterStore = create(
  persist(
    (set) => ({
      count: 1,
      increment: () => set((state) => ({ count: state.count + 1})),
      reset: () => set({ count: 1}),
      setNumber: (number) => set({ count: number })
    }),
    { name: 'counter' }
  )
)
```

<br><br>

## storage 데이터 지우기

```javascript
const clear = () => {
    useCounterStore.persist.clearStorage();
}

return (
    <div>
      <button onClick={clear}>clear</button>
    </div>
  )
```

<br><br>

## DevTools 이용하기

- Zustand는 리덕스 DevTools를 이용할 수 있음

- middleware devtools로 감싸주면 됨

```javascript
import { create } from "zustand";
import { persist, devtools } from 'zustand/middleware'

export const useCounterStore = create(
  persist(
    devtools(
      (set) => ({
        count: 1,
        increment: () => set((state) => ({ count: state.count + 1})),
        reset: () => set({ count: 1}),
        setNumber: (number) => set({ count: number })
      }),
      { name: 'counter' }
    )
  )
)
```

<br><br>

## 소스코드 정리하기
```javascript
import { create } from "zustand";
import { persist, devtools } from 'zustand/middleware'

let counterStore = (set) => ({
  count: 1,
  increment: () => set((state) => ({ count: state.count + 1})),
  reset: () => set({ count: 1}),
  setNumber: (number) => set({ count: number })
})

counterStore = devtools(counterStore);
counterStore = persist(counterStore, { name: 'counter' });

export const useCounterStore = create(counterStore);
```

<br><br>
<br><br>
<br><br>
<br><br>
