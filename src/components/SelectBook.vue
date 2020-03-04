<template>
  <div>
    <div v-if="selected == '書籍'">
      <br />
      <div class="radiobox">
        <input type="radio" id="author" value v-model="author" />
        <label for="author">著者名</label>
        <input type="radio" id="editor" value="編" v-model="author" />
        <label for="editor">編者名</label>
        <div class="box box-author">
          <input ref="author" />
          <span class="name">{{ author }}</span>
        </div>
      </div>

      <div class="box box-year">
        <label>
          <span class="name">出版年</span>
          <input type="number" value="2020" ref="year" />
          <span class="name span-year">年</span>
        </label>
      </div>

      <div class="box">
        <label>
          <span class="name">タイトル</span>
          <input ref="title" />
        </label>
      </div>

      <input type="checkbox" id="subcheckbox" v-model="subChecked" />
      <label for="subcheckbox">
        <span class="name">副題がある場合はチェックを入れてください</span>
      </label>

      <div v-if="subChecked == true">
        <div class="box box-sub">
          <label>
            <span class="name">副題</span>
            <input ref="sub" />
          </label>
        </div>
      </div>

      <div class="box">
        <label>
          <span class="name">出版社</span>
          <input ref="publisher" />
        </label>
      </div>

      <button class="btn-gradation" @click="bookPush">追加</button>
    </div>

    <div v-if="selected == '翻訳書'">
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

      <div class="box box-year">
        <label>
          <span class="name">出版年</span>
          <input type="number" value="2020" ref="year" />
          <span class="name span-year">年</span>
        </label>
      </div>

      <div class="box">
        <label>
          <span class="name">タイトル</span>
          <input ref="title" />
        </label>
      </div>

      <input type="checkbox" id="subcheckbox" v-model="subChecked" />
      <label for="subcheckbox">
        <span class="name">副題がある場合はチェックを入れてください</span>
      </label>

      <div v-if="subChecked== true">
        <div class="box box-sub">
          <label>
            <span class="name">副題</span>
            <input ref="sub" />
          </label>
        </div>
      </div>

      <div class="box box-translator">
        <label>
          <span class="name">訳者名</span>
          <input ref="translator" />
          <span class="name span-translator">訳</span>
        </label>
      </div>

      <div class="box">
        <label>
          <span class="name">出版社</span>
          <input ref="publisher" />
        </label>
      </div>

      <div class="box box-year">
        <label>
          <span class="name">原著年</span>
          <input type="number" value="2020" ref="origin" />
          <span class="name span-year">年</span>
        </label>
      </div>

      <button class="btn-gradation" @click="bookPush">追加</button>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
export default {
  data() {
    return {
      subChecked: false,
      author: "",
      myList: ""
    };
  },
  props: ["selected"],
  methods: {
    bookPush: function() {
      var doc = this.$refs;
      var year = "(" + doc.year.value + ")";
      var title = "『" + doc.title.value + "』";
      var sub = "";

      if (this.subChecked == true) {
        sub = "-" + doc.sub.value;
        title = "『" + doc.title.value + sub + "』";
      }

      var publisher = doc.publisher.value;

      if (this.selected == "書籍") {
        var author = doc.author.value;
        if (this.author != "") {
          author = author + "編";
        }
        this.myList = author + year + title + publisher + ".";
      } else if (this.selected == "翻訳書") {
        var last_jp = doc.last_jp.value + ", ";
        var first_jp = doc.first_jp.value;
        var last_en = "(" + doc.last_en.value + ", ";
        var first_en = doc.first_en.value + ")";
        var translator = "(" + doc.translator.value + "訳)";
        var origin = "(原著は" + doc.origin.value + ")";
        this.myList =
          last_jp +
          first_jp +
          last_en +
          first_en +
          year +
          title +
          translator +
          publisher +
          origin +
          ".";
      }

      this.$emit("book-push", this.myList);

      if (this.selected == "書籍") {
        doc.author.value = this.author = "";
      }
      doc.year.value = "2020";
      doc.title.value = doc.publisher.value = "";

      if (this.subChecked == true) {
        doc.sub.value = "";
        this.subChecked = false;
      }

      if (this.selected == "翻訳書") {
        doc.last_jp.value = doc.first_jp.value = doc.last_en.value = doc.first_en.value = doc.translator.value =
          "";
        doc.origin.value = "2020";
      }
    }
  }
};
</script>

<style scoped>
.radiobox label {
  margin: 0 3px;
}
.box-author {
  position: relative;
  margin-top: 0;
}

.box-author span {
  position: absolute;
  float: right;
  right: 20px;
  bottom: 8px;
}

.box-year {
  position: relative;
}

.box-year label .span-year {
  position: absolute;
  float: right;
  right: 20px;
  bottom: 8px;
}

.box-sub {
  margin-top: 0;
}

.box-translator {
  position: relative;
}

.box-translator .span-translator {
  position: absolute;
  float: right;
  right: 20px;
  bottom: 8px;
}
</style>
