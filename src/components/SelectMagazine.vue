<template>
  <div v-if="selected == '一般雑誌記事'">
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
        <span class="name">記事名</span>
        <input ref="article" />
      </label>
    </div>
    <div class="box">
      <label>
        <span class="name">雑誌名</span>
        <input ref="title" />
      </label>
    </div>
    <div class="box box-add">
      <label>
        <span class="name">号数</span>
        <input type="number" min="1" max="12" ref="issue" />
        <span class="name span-add">月号</span>
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
    <button class="btn-gradation" @click="magazinePush">追加</button>
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
    magazinePush: function() {
      var doc = this.$refs;
      var author = doc.author.value;
      var year = "(" + doc.year.value + ")";
      var article = "｢" + doc.article.value + "｣";
      var title = "『" + doc.title.value + "』";
      var issue = doc.issue.value;
      issue = issue + "月号";
      var page = "､p." + doc.page.value + "､";
      var publisher = doc.publisher.value;
      this.myList =
        author + year + article + title + issue + page + publisher + ".";

      this.$emit("magazine-push", this.myList);

      doc.year.value = "2020";
      doc.author.value = doc.article.value = doc.title.value = doc.issue.value = doc.page.value = doc.publisher.value =
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