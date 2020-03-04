<template>
  <div v-if="selected == '辞書'">
    <br />
    <input type="checkbox" id="authorcheckbox" v-model="authorChecked" checked="checked" />
    <label for="authorcheckbox">
      <span class="name">編者名(いない場合はチェックを外してください)</span>
    </label>
    <br />
    <div class="box box-author">
      <input v-show="authorChecked == true" ref="author" />
      <span v-show="authorChecked== true">
        <span class="name">編</span>
      </span>
    </div>
    <div class="box box-year">
      <label>
        <span class="name">出版年</span>
        <input type="number" value="2020" ref="year" />
        <span class="name">年</span>
      </label>
    </div>
    <div class="box box-title">
      <label>
        <span class="name">タイトル</span>
        <input ref="title" />
        <br />
        <br />
        <span class="prefix">第</span>
        <input class="edition" ref="edition" />
        <span class="prefix">版</span>
      </label>
    </div>
    <div class="box">
      <label>
        <span class="name">出版社</span>
        <input ref="publisher" />
      </label>
    </div>
    <button class="btn-gradation" @click="dictionaryPush">追加</button>
  </div>
</template>

<script>
/* eslint-disable */
export default {
  data() {
    return {
      author: "",
      authorChecked: true,
      myList: ""
    };
  },
  props: ["selected"],
  methods: {
    dictionaryPush: function() {
      var doc = this.$refs;
      var year = "(" + doc.year.value + ")";
      var edition = "(第" + doc.edition.value + "版)";
      var title = "『" + doc.title.value + edition + "』";
      var publisher = doc.publisher.value;

      if (this.authorChecked == true) {
        var author = doc.author.value;
        this.myList = author + year + title + publisher + ".";
      } else {
        this.myList = title + year + publisher + ".";
      }

      this.$emit("dictionary-push", this.myList);

      doc.year.value = "2020";
      doc.author.value = doc.edition.value = doc.title.value = doc.publisher.value =
        "";
      this.authorChecked = true;
    }
  }
};
</script>

<style scoped>
.box-author {
  position: relative;
  margin-top: 0;
}

.box-author span .name {
  position: absolute;
  float: right;
  right: 20px;
  bottom: 8px;
}

.box-year {
  position: relative;
}

.box-year label .name {
  position: absolute;
  float: right;
  right: 20px;
  bottom: 8px;
}

.box-title .prefix {
  font-size: 18px;
  color: #333333;
}

.box-title .edition {
  width: 30px;
  padding: 0;
  text-align: center;
}
</style>