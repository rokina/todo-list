<template>
  <section class="c-container">
    <h1>Todoリスト</h1>
    <div class="c-add__area">
      <input
        type="text"
        name="c-add__name"
        class="c-add__name"
        id="addName"
        placeholder="タスクを入力してください"
      />
      <button id="addButton" class="c-button c-button--green">追加</button>
    </div>
    <div class="c-filter">
      <button class="c-button c-button--gray is-active">全て</button>
      <button class="c-button c-button--gray">作業前</button>
      <button class="c-button c-button--gray">作業中</button>
      <button class="c-button c-button--gray">完了</button>
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
        <tr class="c-lists__body">
          <td>テスト</td>
          <td>2020-04-30 17:00</td>
          <td><button class="c-button c-button--yet">作業前</button></td>
          <td><button class="c-button c-button--delete">削除</button></td>
        </tr>
      </tbody>
    </table>
  </section>
</template>

<script>
export default {};
</script>

<style>
</style>
