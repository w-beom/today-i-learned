
# 커스텀 이벤트
컴포넌트 및 props와는 달리, 이벤트는 자동 대소문자 변환을 제공하지 않습니다.<br> 
emit할 이벤트의 이름은 자동 대소문자 변환을 사용하는 것 대신 정확한 이름을 사용하여야 합니다.

# 커스텀 이벤트 정의
emits 옵션을 사용하여 커스텀 이벤트를 정의한다.
- MyComponent.vue
```javascript
<template>
  <div>
    {{ title }}
    <br />
    <input type="button" @click="onClick" value="Click Me" />
    <br />
    <input type="button" @click="onAnotherClick" value="Click Me, again" />
  </div>
</template>
<script>
import { defineComponent, reactive } from "vue";

export default defineComponent({
  props: ["title"],
  emits: ["update", "anotherUpdate"],

  setup(props, { emit }) {
    const user = reactive({
      name: "홍길동",
      age: 11,
    });

    //event
    const onClick = function () {
      console.log("Click'");
      emit("update", user);
    };

    const onAnotherClick = () => {
      emit("anotherUpdate", "바보");
    };
    return { onClick, onAnotherClick };
  },
});
</script>

```
- MyContainer.vue
```javascript
<template>
  <my-navi @selected="onSelected"></my-navi>
  <my-component
    @update="onUpdate"
    @anotherUpdate="onAnotherUpdate"
    :title="selectedMenu"
  ></my-component>
</template>
<script>
import { defineComponent, reactive, ref } from "vue";
import MyComponent from "@/components/c04/MyComponent.vue";
import MyNavi from "@/components/c04/MyNavi.vue";

export default defineComponent({
  components: { MyComponent, MyNavi },
  setup(props, { emit }) {
    const selectedMenu = ref("");

    const onUpdate = (res) => {
      console.log("Update event occured.");
    };

    const onAnotherUpdate = (data) => {
      console.log(data);
    };

    const onSelected = (data) => {
      console.log("the sended data is " + data);
      selectedMenu.value = data; // 값을 설정
    };

    return { onUpdate, onAnotherUpdate, onSelected, selectedMenu };
  },
});
</script>

```
- MyNavi.vue
```javascript
<template>
  <div>
    <div @click="onSelected('1')">전체쪽지</div>
    <div @click="onSelected('2')">받은쪽지</div>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  emits: ["selected"],
  setup(props, { emit }) {
    //event
    const onSelected = (selectedVal) => {
      console.log("the selcted value is : " + selectedVal);
      emit("selected", selectedVal);
    };

    return { onSelected };
  },
});
</script>

```
# Computed 변수

# Watch

# v-model 동작원리
