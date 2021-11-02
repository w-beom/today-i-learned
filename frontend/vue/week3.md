# 3주차
# V-Model
## input & textarea
```javascript
<template>
  <div>
    hello <br>
    <input type="text" v-model="message" />
    <br>
    <input type="text" v-model="name" />
    <br>
    <input type="text" v-model="age">
    <br>
    {{message}}
    <br>
    이름 : {{name}}
    <br>
    나이 : {{age}}
  </div>
</template>

<script>
import { defineComponent, reactive, ref, toRefs } from "vue";

export default defineComponent({
  setup() {
    const message = ref("111111");
    const userInfo = reactive({
        name : "kim",
        age :11
    })

    const {name,age} = toRefs(userInfo)

    return {
      message,
      name,
      age
    };
  },
});
</script>
```
## radioBox
```javascript
<template>
    <div>
        <input type="radio" id="one" value="One" v-model="picked">
        <label for="one">One</label>
        <input type="radio" id="two" value="Two" v-model="picked">
        <label for="two">Two</label>
        <br>
        {{picked}}
    </div>
</template>
<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  setup() {
      const picked = ref("");
      return {
          picked
      };
  },
});
</script>
```
##checkBox
- MyCheckVue
```javascript
<template>
    <div>
        <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
        <label for="jack">Jack</label>
        <input type="checkbox" id="john" value="John" v-model="checkedNames">
        <label for="john">John</label>
        <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
        <label for="mike">Mike</label>
        <br>
        {{checkedNames}}
    </div>
</template>

<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
    setup() {
        const checkedNames = ref([])
        return {
            checkedNames
        }
        
    },
})
</script>
```

## select
- v-bind:value 와 :value 는 같은 문법
```javascript
<template>
  <div>
    <select v-model="selected">
      <option diabled value="">Please select one</option>
      <option v:bind:value="optA">{{ optA }}</option>
      <option :value="optB">{{ optB }}</option>
      <option :value="optC">{{ optC }}</option>
    </select>
    <br />
    {{ selected }}
  </div>
</template>

<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  setup() {
    const optA = ref("a");
    const optB = ref("b");
    const optC = ref("c");

    const selected = ref("");
    return {
      selected,
      optA,
      optB,
      optC,
    };
  },
});
</script>
```
- v-for를 이용한 option 태그 그리기
```javascript
<template>
  <div>
    <select v-model="selected">
      <option value="">선택하세요</option>
      <option :value="item.key" v-for="item in myOptions">
        {{ item.value }}
      </option>
    </select>
    <br />
    {{ selected }}
  </div>
</template>
<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  setup() {
    const selected = ref("");
    const myOptions = ref([
      { key: "1", value: "사과" },
      { key: "2", value: "배" },
    ]);

    return {
      selected,
      myOptions,
    };
  },
});
</script>
```
## Mutilple Select
```javascript
<template>
  <div>
    <select multiple v-model="selected">
      <option disabled value="">선택하세요</option>
      <option :value="item.key" v-for="item in myOptions">
        {{ item.value }}
      </option>
    </select>
    <br />
    {{ selected }}
  </div>
</template>
<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  setup() {
    const selected = ref([]);
    const myOptions = ref([
      { key: "1", value: "사과" },
      { key: "2", value: "배" },
    ]);

    return {
      selected,
      myOptions,
    };
  },
});
</script>
```

## click event  (radio button)
```javascript
<template>
  <div>
    <input type="radio" id="one" value="One" v-model="picked" />
    <label for="one">One</label>
    <input type="radio" id="two" value="Two" v-model="picked" />
    <label for="two">Two</label>
    <br />
    {{ picked }}
    <br />
    <input type="button" @click="onClick" value="Click Me" />
  </div>
</template>
<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  setup() {
    const picked = ref("");

    //event handlers
    const onClick = () => {
        picked.value = "Two";
    };

    return {
      picked,
      onClick
    };
  },
});
</script>
```
# Props
## 기초
마치 HTML 요소의 속성인 것처럼 사용할 수 있어 부모 컴포넌트에서 자식 컴포넌트에 값을 전달 할 수 있다.
- MyProps.vue
```javascript
<template>
  <div>
    <h2>나는 {{ title }} 자식입니다. 나이는 {{age}}입니다.</h2>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  props: ["title", "age"],
  setup() {
    return {};
  },
});
</script>
```
- App.vue
```javascript
<script setup>
import MyProps from '@/components/c02/MyProps.vue'
</script>

<template>
  <my-props title="개" age="10"></my-props>
</template>

<style>
</style>
```
HTML 속성으로 값을 전달할 수 있다.
## script에서 props값 사용하기
```javascript
<template>
  <div>
    <h2>나는 {{ title }} 자식입니다. 나이는 {{ age }}입니다.</h2>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  props: ["title", "age"],
  setup(props, { emit }) {
    console.log(props.title); 
    console.log(props.age);
    return {};
  },
});
</script>
```
setup 함수 파라미터에 props를 전달해 값을 사용할 수 있다.
### prop 타입 설정하기
```javascript
<template>
  <div>
    <h2>나는 {{ title }} 자식입니다. 나이는 {{ age }}입니다.</h2>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    title: String,
    age: Number,
  },
  setup(props, { emit }) {
    console.log(props.title);
    console.log(props.age);
    return {};
  },
});
</script>
```
### 세부 설정하기
```javascript
<template>
  <div>
    <h2>나는 {{ title }} 자식입니다. 나이는 {{ age }}입니다.</h2>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    title: {
      type: String,
      required: true,
      default: "Dog",
    },
    age: {
      type: Number,
      required: false,
      default: 0,
    },
  },
  setup(props, { emit }) {
    console.log(props.title);
    console.log(props.age);
    return {};
  },
});
</script>
```
## 단방향 데이터 흐름
모든 props는 자식 속성과 부모 속성간에 단방향으로 데이터를 전달한다.

## 정적/동적 Prop전달

## Component 동적 생성?
```javascript
<template>
  <div>
    <my-select></my-select>
    <my-props :title="childTitle" detail-addr="개집" age="12"></my-props>
  </div>
</template>

<script>
import { defineComponent,ref } from "vue";
import MyProps from "../c02/MyProps.vue";
import MySelect from "../c02/MySelect.vue";

export default defineComponent({
  components: {
    MyProps,
    MySelect,
  },
  setup() {
    const childTitle = ref("");
    childTitle.value = "대통령";
    return {
      childTitle,
    };
  },
});
</script>
```