<template>
  <form @submit.prevent="handleSubmitNewTodo">
    <input
      type="text"
      placeholder="Add new todo"
      required
      class="form-control px-5 py-4"
      v-model.trim="state.title"
      @change="$emit('update:newTodoTitle', $event.target.value)"
    />
  </form>
</template>

<script lang="ts">
import { defineComponent, PropType, reactive, watch } from "vue";

export type HandleSubmitNewTodo = () => void;

type State = {
  title: string;
};

export default defineComponent({
  props: {
    newTodoTitle: {
      type: String as PropType<string>,
      required: true
    },
    handleSubmitNewTodo: {
      type: Function as PropType<HandleSubmitNewTodo>,
      required: true
    }
  },

  emits: ["update:newTodoTitle"],

  setup(props) {
    const state = reactive<State>({ title: props.newTodoTitle });
    watch(
      () => props.newTodoTitle,
      newValue => {
        state.title = newValue;
      }
    );
    return { state };
  }
});
</script>
