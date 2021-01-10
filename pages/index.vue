<template>
  <section class="c-container">
    <h1>Todoリスト</h1>
    <div class="c-add__area">
      <input
        type="text"
        name="addName"
        class="c-add__name"
        id="addName"
        v-model="content"
        placeholder="タスクを入力してください"
      />
      <button id="addButton" class="c-button -green" @click="insert">
        追加
      </button>
    </div>
    <div class="c-filter">
      <button
        class="c-button -gray"
        :class="{ 'is-active': !find_flg }"
        @click="flag_reset"
      >
        全て
      </button>
      <button
        class="c-button -gray"
        :class="{ 'is-active': find_flg && find_state == '作業前' }"
        @click="find('作業前')"
      >
        作業前
      </button>
      <button
        class="c-button -gray"
        :class="{ 'is-active': find_flg && find_state == '作業中' }"
        @click="find('作業中')"
      >
        作業中
      </button>
      <button
        class="c-button -gray"
        :class="{ 'is-active': find_flg && find_state == '完了' }"
        @click="find('完了')"
      >
        完了
      </button>
    </div>
    <table class="c-lists">
      <thead>
        <tr class="c-lists__head">
          <th>タスク</th>
          <th>登録日時</th>
          <th>状態</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr
          class="c-lists__body"
          v-for="(item, index) in display_todos"
          :key="index"
        >
          <td>{{ item.content }}</td>
          <td>{{ item.created }}</td>
          <td>
            <button
              class="c-button"
              :class="{
                '-yet': item.state == '作業前',
                '-progress': item.state == '作業中',
                '-done': item.state == '完了',
              }"
              @click="changeState(item)"
            >
              {{ item.state }}
            </button>
          </td>
          <td>
            <button class="c-button -delete" @click="remove(item)">削除</button>
          </td>
        </tr>
      </tbody>
    </table>
  </section>
</template>

<script>
import { mapState } from "vuex";

export default {
  data: function () {
    return {
      content: "",
      find_state: "",
      find_flg: false,
    };
  },
  computed: {
    ...mapState(["todos"]),
    display_todos: function () {
      if (this.find_flg) {
        let arr = [];
        let data = this.todos;
        data.forEach((element) => {
          if (element.state == this.find_state) {
            arr.push(element);
          }
        });
        return arr;
      } else {
        return this.todos;
      }
    },
  },
  methods: {
    insert: function () {
      if (this.content != "") {
        this.$store.commit("insert", { content: this.content });
        this.content = "";
      }
    },
    remove: function (todo) {
      this.$store.commit("remove", todo);
    },
    changeState: function (todo) {
      this.$store.commit("changeState", todo);
    },
    find: function (findState) {
      this.find_state = findState;
      this.find_flg = true;
    },
    flag_reset: function () {
      this.find_flg = false;
    },
  },
};
</script>

<style>
</style>
