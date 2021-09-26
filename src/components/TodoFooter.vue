<template>
  <div class="todo-footer">
    <div class="todo-left">
      <span v-if="active > 0">{{ active }} items left</span>
      <span v-else>All todos completed</span>
    </div>
    <div class="todo-filter">
      <span @click="$emit('change-type', 'all')" :class="{ active: type === 'all' }">All</span>
      <span @click="$emit('change-type', 'active')" :class="{ active: type === 'active' }">Active</span>
      <span @click="$emit('change-type', 'completed')" :class="{ active: type === 'completed' }"
        >Completed</span
      >
    </div>
    <div class="todo-clear">
      <span @click="$emit('clear-completed')">Clear Completed</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoFooter",
  props: {
    active: Number,
    type: String,
  },
};
</script>

<style lang="scss">
.todo-footer {
  display: grid;
  grid-template-areas: "left filter clear";
  grid-template-rows: 50px;
  grid-template-columns: 30% 40% 30%;
  border-bottom-left-radius: 5px;
  border-bottom-right-radius: 5px;
  color: hsl(236, 14%, 38%);
  font-size: 13px;
  font-weight: 700;

  & > div {
    place-self: center;
  }

  .todo-left {
    grid-area: left;
  }

  .todo-clear {
    grid-area: clear;
  }

  .todo-filter {
    grid-area: filter;

    > span {
      transition: all 300ms;
      margin: 0 10px;
      cursor: pointer;

      &.active {
        color: hsl(220, 98%, 61%);
      }

      &:not(.active):hover {
        color: hsl(236, 9%, 61%);
      }
    }
  }

  .todo-clear {
    cursor: pointer;
  }
}

@media screen and (max-width: 992px) {
  .todo-footer {
    grid-template-areas:
      "left clear"
      "filter filter";
    grid-template-columns: 50% 50%;
    background-color: transparent !important;
    font-size: 14px;

    & > div {
      display: flex;
      align-items: center;
      justify-content: center;
      background-color: hsl(235, 24%, 19%);
      place-self: inherit;
    }

    .todo-left {
      border-bottom-left-radius: 5px;
    }

    .todo-clear {
      border-bottom-right-radius: 5px;
    }

    .todo-filter {
      border-radius: 5px;
      height: 50px;
      font-size: 16px;
    }
  }
}
</style>
