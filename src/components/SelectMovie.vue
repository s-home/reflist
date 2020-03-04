<template>
  <div v-if="selected == '映画'">
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
    <div class="box">
      <label>
        <span class="name">タイトル(日)</span>
        <input ref="title_jp" />
      </label>
    </div>
    <div class="box">
      <label>
        <span class="name">タイトル(英)</span>
        <input ref="title_en" />
      </label>
    </div>
    <div class="box">
      <label>
        <span class="name">発行機関</span>
        <input ref="publisher" />
      </label>
    </div>
    <button class="btn-gradation" @click="moviePush">追加</button>
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
    moviePush: function() {
      var doc = this.$refs;
      var last_jp = doc.last_jp.value + ", ";
      var first_jp = doc.first_jp.value;
      var last_en = "(" + doc.last_en.value + ", ";
      var first_en = doc.first_en.value + ")";
      var title_jp = "『" + doc.title_jp.value;
      var title_en = "(" + doc.title_en.value + ")";
      var publisher = doc.publisher.value;
      this.myList =
        last_jp +
        first_jp +
        last_en +
        first_en +
        "(製作･監督･脚本)" +
        title_jp +
        title_en +
        "』" +
        "[映画]､" +
        publisher +
        ".";

      this.$emit("movie-push", this.myList);

      doc.last_jp.value = doc.first_jp.value = doc.last_en.value = doc.first_en.value = doc.title_jp.value = doc.title_en.value = doc.publisher.value =
        "";
    }
  }
};
</script>