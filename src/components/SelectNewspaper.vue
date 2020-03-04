<template>
  <div v-if="selected == '新聞記事'">
    <div class="box">
      <label>
        <span class="name">新聞名</span>
        <input ref="newspaper" />
      </label>
    </div>
    <div class="box">
      <label>
        <span class="name">記事名</span>
        <input ref="article" />
      </label>
    </div>
    <div class="box">
      <span class="name">発行日</span>
      <br />
      <input type="number" min="1" ref="year" value="2020" style="width:80px;" />
      <span class="name">年</span>
      <input type="number" min="1" max="12" ref="month" style="width:60px;" />
      <span class="name">月</span>
      <input type="number" min="1" max="31" ref="day" style="width:60px;" />
      <span class="name">日</span>
    </div>
    <div class="radiobox">
      <input type="radio" id="morning" value="朝刊" v-model="time" />
      <label for="morning" style="margin-left:5px;">朝刊</label>
      <br />
      <input type="radio" id="evening" value="夕刊" v-model="time" />
      <label for="evening" style="margin-left:5px;">夕刊</label>
    </div>
    <div class="box">
      <input type="number" min="1" ref="edition" style="width:60px;" />版
      <input type="number" min="1" ref="side" style="width:60px;" />面
    </div>
    <button class="btn-gradation" @click="newspaperPush">追加</button>
  </div>
</template>

<script>
/* eslint-disable */
export default {
  data() {
    return {
      myList: "",
      time: "朝刊"
    };
  },
  props: ["selected"],
  methods: {
    newspaperPush: function() {
      var doc = this.$refs;
      var newspaper = doc.newspaper.value;
      var article = doc.article.value;
      var year = doc.year.value;
      var month = doc.month.value;
      var day = doc.day.value;
      var time = this.time;
      var edition = doc.edition.value;
      var side = doc.side.value;
      this.myList =
        "｢" +
        article +
        "｣" +
        "(" +
        year +
        "､" +
        month +
        "月" +
        day +
        "日)『" +
        newspaper +
        "』" +
        time +
        "､" +
        edition +
        "版､" +
        side +
        "面.";

      this.$emit("newspaper-push", this.myList);

      doc.newspaper.value = doc.article.value = doc.month.value = doc.day.value = doc.edition.value = doc.side.value =
        "";
      doc.year.value = "2020";
      this.time = "朝刊";
    }
  }
};
</script>