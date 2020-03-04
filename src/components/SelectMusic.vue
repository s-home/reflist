<template>
  <div v-if="selected == '音楽'">
    <div class="box">
      <label>
        <span class="name">名</span>
        <input ref="first_jp" />
      </label>
    </div>
    <div class="box">
      <label>
        <span class="name">姓</span>
        <input ref="last_jp" />
      </label>
    </div>
    <div class="box">
      <label>
        <span class="name">First Name</span>
        <input ref="first_en" />
      </label>
    </div>
    <div class="box">
      <label>
        <span class="name">Last Name</span>
        <input ref="last_en" />
      </label>
    </div>
    <div class="box box-add">
      <label>
        <span class="name">出版年</span>
        <input type="number" value="2020" ref="year" />
        <span class="name span-add">年</span>
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
        <span class="name">収録CD名</span>
        <input ref="cd" />
      </label>
    </div>
    <div class="box">
      <label>
        <span class="name">発行機関</span>
        <input ref="publisher" />
      </label>
    </div>
    <div class="box box-add">
      <label>
        <span class="name">録音年</span>
        <input type="number" value="2020" ref="record" />
        <span class="name span-add">年</span>
      </label>
    </div>
    <button class="btn-gradation" @click="musicPush">追加</button>
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
    musicPush: function() {
      var doc = this.$refs;
      var last_jp = doc.last_jp.value + ", ";
      var first_jp = doc.first_jp.value;
      var last_en = "(" + doc.last_en.value + ", ";
      var first_en = doc.first_en.value + ")";
      var year = "(" + doc.year.value + ")";
      var title = "｢" + doc.title.value + "｣";
      var cd = "『" + doc.cd.value + "』";
      var publisher = doc.publisher.value;
      var record = "(" + doc.record.value + "録音)";
      this.myList =
        last_jp +
        first_jp +
        last_en +
        first_en +
        year +
        title +
        cd +
        "[CD]" +
        publisher +
        record +
        ".";

      this.$emit("music-push", this.myList);

      doc.last_jp.value = doc.first_jp.value = doc.last_en.value = doc.first_en.value = doc.title.value = doc.cd.value = doc.publisher.value =
        "";
      doc.year.value = doc.record.value = "2020";
    }
  }
};
</script>

<style scoped>
.box-add {
  position: relative;
}

.span-add {
  position: absolute;
  float: right;
  right: 20px;
  bottom: 8px;
}
</style>