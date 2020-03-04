<template>
  <div v-if="selected == 'パンフレット'">
    <div class="box">
      <label>
        <span class="name">著者名</span>
        <input ref="author" />
      </label>
    </div>
    <div class="box box-add">
      <label>
        <span class="name">発行年</span>
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
        <span class="name">発行機関</span>
        <input ref="publisher" />
      </label>
    </div>
    <button class="btn-gradation" @click="pamphletPush">追加</button>
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
    pamphletPush: function() {
      var doc = this.$refs;
      var author = doc.author.value;
      var year = "(" + doc.year.value + ")";
      var title = "｢" + doc.title.value + "｣";
      var publisher = doc.publisher.value;
      this.myList = author + year + title + "[パンフレット]" + publisher + ".";
      this.$emit("pamphlet-push", this.myList);
      doc.author.value = doc.title.value = doc.publisher.value = "";
      doc.year.value = "2020";
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