<template>
  <div v-if="selected == '学術誌論文'">
    <div class="box">
      <label>
        <span class="name">著者名</span>
        <input ref="author" />
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
        <span class="name">掲載書籍名</span>
        <input ref="book" />
      </label>
    </div>
    <div class="box box-add">
      <label>
        <span class="name">号数</span>
        <input type="number" min="1" ref="issue" />
        <span class="name span-add">号</span>
      </label>
    </div>
    <div class="box">
      <label>
        <span class="name">ページ数</span>
        <input type="number" min="1" ref="page" />
      </label>
    </div>
    <div class="box">
      <label>
        <span class="name">出版社</span>
        <input ref="publisher" />
      </label>
    </div>
    <button class="btn-gradation" @click="essayPush">追加</button>
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
    essayPush: function() {
      var doc = this.$refs;
      var author = doc.author.value;
      var year = "(" + doc.year.value + ")";
      var title = "｢" + doc.title.value + "｣";
      var book = "『" + doc.book.value + "』";
      var issue = doc.issue.value;
      issue = issue + "号";
      var page = "､p." + doc.page.value + "､";
      var publisher = doc.publisher.value;
      this.myList =
        author + year + title + book + issue + page + publisher + ".";

      this.$emit("essay-push", this.myList);

      doc.year.value = "2020";
      doc.author.value = doc.title.value = doc.book.value = doc.issue.value = doc.page.value = doc.publisher.value =
        "";
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