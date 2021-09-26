<template>
  <div class="todo-item" :class="{ active: completed }">
    <span class="todo-circle" @click="$emit('toggle-complete', id)">
      <img v-if="completed" src="../assets/images/icon-check.svg" alt="Checked Icon" />
    </span>
    <span class="todo-title">{{ title }}</span>
    <span class="todo-remove" @click="$emit('remove-todo', id)">
      <img src="../assets/images/icon-cross.svg" alt="Cross Icon" />
    </span>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    id: Number,
    title: String,
    completed: Boolean,
  },
};
</script>

<style lang="scss">
.todo-item {
  display: flex;
  align-items: center;
  padding-left: 20px;
  height: 60px;
  color: hsl(236, 15%, 65%);

  .todo-circle {
    display: flex;
    flex-shrink: 0;
    align-items: center;
    justify-content: center;
    margin-right: 20px;
    border: 2px solid hsl(235, 21%, 32%);
    border-radius: 100%;
    cursor: pointer;
    width: 23px;
    height: 23px;
  }

  .todo-title {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }

  .todo-remove {
    transition: all 300ms;
    opacity: 0;
    margin-right: 20px;
    margin-left: auto;
    cursor: pointer;
  }

  &.active {
    text-decoration: line-through;
    color: hsl(235, 15%, 30%);

    .todo-circle {
      img {
        width: 13px;
      }
    }
  }

  &.active .todo-circle,
  &:not(.active) .todo-circle:hover {
    border: 0;
    background: linear-gradient(135deg, hsl(192, 100%, 67%), hsl(280, 87%, 65%));
  }

  &:not(.active) .todo-circle:hover {
    position: relative;

    &::before {
      position: absolute;
      top: 2px;
      left: 2px;
      border-radius: 100%;
      background-color: hsl(235, 24%, 19%);
      width: 19px;
      height: 19px;
      content: "";
    }
  }

  &:hover {
    .todo-remove {
      opacity: 1;
    }
  }
}
</style>
