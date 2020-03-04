<template>
  <div>
    <div class="headline" v-if="selected == ''">
      <h1 class="subtitle">参考文献リスト自動作成</h1>
      <h1 class="maintitle">RefList</h1><br>
      <p>参考文献リストを作成する時</p>
      <p>書式をいちいち調べていませんか？</p>
      <p>そんな日々とはもうおさらばです</p>
      <p class="lets">さあ、下から文献の種類を選択して始めよう</p>
      <p class="arrow">⬇︎</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["types", "selected"]
}
</script>

<style scoped>

.headline {
  margin-top: 40px;
  text-align: center;
}

.subtitle {
  text-align:center;
  color:darkturquoise;
}

.maintitle {
  text-align: center;
  font-size: 120px;
  font-family: cursive;
  color: turquoise;
}

.lets {
  margin-bottom: 30px;
  font-family: 'Yu Gothic'
}

.arrow {
  text-align: center;
  color: darkturquoise;
  font-size: 50px;
}

</style>
