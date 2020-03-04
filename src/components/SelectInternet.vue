<template>
  <div v-if="selected == 'インターネット'">
    <div class="box">
      <label>
        <span class="name">サイト名</span>
        <input ref="site" />
      </label>
    </div>
    <div class="box">
      <label>
        <span class="name">タイトル</span>
        <input ref="title" />
      </label>
    </div>
    <div class="box">
      <label>
        <span class="name">URL</span>
        <input ref="url" />
      </label>
    </div>
    <div class="box">
      <label>
        <span class="name">閲覧日</span>
        <br />
        <input type="number" min="1" ref="year" value="2020" style="width:80px;" />
        <span class="name">年</span>
        <input type="number" min="1" max="12" ref="month" style="width:60px;" />
        <span class="name">月</span>
        <input type="number" min="1" max="31" ref="day" style="width:60px;" />
        <span class="name">日</span>
      </label>
    </div>
    <button class="btn-gradation" @click="internetPush">追加</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      myList: ""
    };
  },
  props: ["selected"],
  methods: {
    internetPush: function() {
      var doc = this.$refs;
      var site = doc.site.value;
      var title = "｢" + doc.title.value + "｣";
      var url = doc.url.value;
      var year = "(" + doc.year.value + "､";
      var month = doc.month.value + "月";
      var day = doc.day.value + "日閲覧)";
      this.myList = site + title + url + year + month + day + ".";

      this.$emit("internet-push", this.myList);

      doc.site.value = doc.title.value = doc.url.value = doc.month.value = doc.day.value =
        "";
      doc.year.value = "2020";
    }
  }
};
</script>

<style scoped>
</style>