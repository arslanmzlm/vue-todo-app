<template>
  <div class="add-todo">
    <div class="input-add">
      <span class="input-circle"></span>
      <input type="text" v-model="title" placeholder="Type something..." @keypress.enter="addTodo" />
    </div>
    <div v-if="title.length > 0" class="add-helper">
      press enter for adding.
    </div>
  </div>
</template>

<script>
export default {
  name: "AddTodo",
  data() {
    return {
      title: "",
    };
  },
  methods: {
    addTodo: function() {
      this.$emit("add-todo", this.title);
      this.title = "";
    },
  },
};
</script>

<style lang="scss">
.add-todo {
  margin-bottom: 25px;

  .input-add {
    position: relative;
    box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15);

    .input-circle {
      display: inline-block;
      position: absolute;
      top: 50%;
      left: 20px;
      transform: translateY(-50%);
      border: 2px solid hsl(235, 21%, 32%);
      border-radius: 100%;
      width: 23px;
      height: 23px;
    }

    input {
      border: 0;
      border-radius: 5px;
      background-color: hsl(235, 24%, 19%);
      padding-left: 57px;
      width: 100%;
      height: 60px;
      color: hsl(235, 41%, 88%);
      font-size: 18px;

      &:focus {
        outline: none;
      }

      &::placeholder {
        color: hsl(236, 15%, 65%);
      }
    }
  }

  .add-helper {
    margin-top: 4px;
    text-align: right;
    font-size: 14px;
  }
}
</style>
