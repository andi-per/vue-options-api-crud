<template>
  <div style="margin-top: 20px">
    <ul class="list-group">
      <li
        class="list-group-item"
        v-for="(item, index) in todoList"
        :key="index"
      >
        <div class="row">
          <div class="col">
            <span v-if="item.isDone"
              ><del>{{ item.activity }}</del></span
            >
            <span v-else>{{ item.activity }}</span>
          </div>
          <div class="col-auto">
            <div class="row gx-2">
              <div class="col">
                <button class="btn btn-success" @click="markDone(index)">
                  Done
                </button>
              </div>
              <div class="col">
                <button class="btn btn-danger" @click="deleteTodo(index)">
                  X
                </button>
              </div>
            </div>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  props: {
    todoList: {
      type: Array,
      default: [],
    },
  },
  methods: {
    deleteTodo(index) {
      this.$emit("deleteTodo", index);
    },
    markDone(index) {
      this.$emit("markDone", index);
    },
  },
};
</script>
<style lang=""></style>
