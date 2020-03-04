<template>
  <div id="app">
    <Header />
    <div class="container">
      <Headline :types="types" :selected="selected" />

      <select style="margin-bottom:30px;" v-model="selected">
        <option disabled value>参考文献の種類を選択してください</option>
        <option v-for="type in types" :key="type">{{ type }}</option>
      </select>

      <SelectBook :selected="selected" @book-push="refPush($event)" />
      <SelectDictionary :selected="selected" @dictionary-push="refPush($event)" />
      <SelectMagazine :selected="selected" @magazine-push="refPush($event)" />
      <SelectEssay :selected="selected" @essay-push="refPush($event)" />
      <SelectNewspaper :selected="selected" @newspaper-push="refPush($event)" />
      <SelectPamphlet :selected="selected" @pamphlet-push="refPush($event)" />
      <SelectMusic :selected="selected" @music-push="refPush($event)" />
      <SelectMovie :selected="selected" @movie-push="refPush($event)" />
      <SelectInternet :selected="selected" @internet-push="refPush($event)" />

      <br />

      <div id="copy"></div>

      <tr v-for="item in refs" :key="item">
        <td class="items" style="font-size:12px;text-align:center;">{{item}}</td>
        <button class="btn-push" @click="copy(item)">コピー</button>
        <button class="btn-push" @click="remove(item)">削除</button>
      </tr>

      <br />

      <div class="buttons" v-if="refs != ''">
        <button class="btn-open" @click="allCopy">すべてコピー</button>
        <button class="btn-open" @click="allRemove">すべて削除</button>
      </div>
    </div>
    <Footer></Footer>
  </div>
</template>

<script>
/* eslint-disable */

import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import Headline from "./components/Headline.vue";
import SelectBook from "./components/SelectBook.vue";
import SelectDictionary from "./components/SelectDictionary.vue";
import SelectMagazine from "./components/SelectMagazine.vue";
import SelectEssay from "./components/SelectEssay.vue";
import SelectNewspaper from "./components/SelectNewspaper.vue";
import SelectPamphlet from "./components/SelectPamphlet";
import SelectMusic from "./components/SelectMusic";
import SelectMovie from "./components/SelectMovie";
import SelectInternet from "./components/SelectInternet";

export default {
  data() {
    return {
      selected: "",
      types: [
        "書籍",
        "翻訳書",
        "辞書",
        "一般雑誌記事",
        "学術誌論文",
        "新聞記事",
        "パンフレット",
        "音楽",
        "映画",
        "インターネット"
      ],
      refs: []
    };
  },
  mounted() {
    if (localStorage.getItem("refs")) {
      try {
        this.refs = JSON.parse(localStorage.getItem("refs"));
      } catch (e) {
        localStorage.removeItem("refs");
      }
    }
  },
  components: {
    Header,
    Footer,
    Headline,
    SelectBook,
    SelectDictionary,
    SelectMagazine,
    SelectEssay,
    SelectNewspaper,
    SelectPamphlet,
    SelectMusic,
    SelectMovie,
    SelectInternet
  },
  methods: {
    refPush: function(value) {
      this.refs.push(value);
      this.save();
    },
    remove: function(item) {
      var index = this.refs.indexOf(item);
      this.refs.splice(index, 1);
      this.save();
    },
    copy: function(item) {
      if (navigator.userAgent.match(/(ipad|ipod|iphone|Android)/i)) {
        // HTMLTextAreaElement オブジェクトを作成する
        var div = document.getElementById("copy");
        var add = document.createElement("input");
        add.setAttribute("type", "text");
        add.setAttribute("value", item);
        add.setAttribute("id", "qwerty");
        div.appendChild(add);

        // readOnlyを外す
        div.readOnly = false;
        add.readOnly = false;
        // ここから下が、iOS用でしか機能しない関数------
        var range = document.createRange();
        range.selectNode(qwerty);
        window.getSelection().addRange(range);
        // ------------------------------------------
        document.execCommand("copy");
        // readOnlyに戻す
        add.readOnly = true;
        div.readOnly = true;
        div.removeChild(add);
        alert("コピーしました。");
      } else {
        navigator.clipboard.writeText(item);
      }
    },
    allCopy: function() {
      var copyText = this.refs.join("\n");

      if (navigator.userAgent.match(/(ipad|ipod|iphone|Android)/i)) {
        copyText = this.refs.join("\n");
        var div = document.getElementById("copy");
        var add = document.createElement("input");
        add.setAttribute("type", "text");
        add.setAttribute("value", copyText);
        add.setAttribute("id", "qwerty");
        div.appendChild(add);

        div.readOnly = false;
        add.readOnly = false;
        var range = document.createRange();
        range.selectNode(qwerty);
        window.getSelection().addRange(range);
        document.execCommand("copy");
        add.readOnly = true;
        div.readOnly = true;
        div.removeChild(add);
        alert("コピーしました。");
      } else {
        navigator.clipboard.writeText(copyText);
      }
    },
    allRemove: function() {
      if (this.refs.length == 0) {
        return;
      }
      if (window.confirm("本当によろしいですか？")) {
        this.refs = [];
        this.save();
      }
    },
    save: function() {
      const parsed = JSON.stringify(this.refs);
      localStorage.setItem("refs", parsed);
    }
  }
};
</script>

<style>
* {
  margin: 0;
  background-color: #f9ffff;
}

.container {
  min-height: 100vh;
  margin: 0 30vw;
}

.box {
  margin: 25px 0;
}
.box input {
  font: 15px/24px sans-serif;
  box-sizing: border-box;
  width: 100%;
  padding: 0.3em;
  padding-left: 1em;
  transition: 0.3s;
  letter-spacing: 1px;
  color: dimgray;
  border: none;
  border-bottom: 2px solid turquoise;
  background: transparent;
}
.box input:focus {
  border-bottom: 2px solid aqua;
  outline: none;
}

.name {
  font-size: 14px;
  color: #333333;
}

.btn-open {
  display: inline-block;
  width: 180px;
  height: 50px;
  text-align: center;
  background-color: darkturquoise;
  font-size: 16px;
  line-height: 52px;
  color: #fff;
  text-decoration: none;
  font-weight: bold;
  border: 2px solid darkturquoise;
  position: relative;
  overflow: hidden;
  z-index: 1;
  border-radius: 10px;
  outline: none;
}
.btn-open:after {
  width: 100%;
  height: 0;
  content: "";
  position: absolute;
  top: 50%;
  left: 50%;
  background: #fff;
  opacity: 0;
  transform: translateX(-50%) translateY(-50%) rotate(45deg);
  transition: 0.2s;
  z-index: -1;
}
.btn-open:hover {
  color: darkturquoise;
}
.btn-open:hover:after {
  height: 240%;
  opacity: 1;
}
.btn-open:active:after {
  transition: 0s;
  height: 340%;
  opacity: 1;
}

.buttons {
  display: flex;
  justify-content: space-around;
}

.btn-push {
  display: inline-block;
  text-align: left;
  background-color: #00bcd4;
  color: #fff;
  text-decoration: none;
  outline: none;
  border-radius: 4px;
  border-bottom: 4px solid #118e9e;
}

.btn-push:active {
  transform: translateY(4px);
  border-bottom: none;
}

.btn-gradation {
  margin: 10px;
  padding: 5px 10px;
  width: 30%;
  text-align: center;
  transition: 0.5s;
  background-size: 200% auto;
  color: white;
  box-shadow: 0 0 20px #eee;
  border-radius: 10px;
  display: block;
  outline: none;
  font-weight: bold;
  font-size: 18px;
  background-image: linear-gradient(
    to right,
    deepskyblue 0%,
    #26d0ce 51%,
    #1a2980 100%
  );
}

.btn-gradation:hover {
  background-position: right center;
}

select {
  width: 100%;
  height: 40px;
  font-size: 16px;
  margin-top: 30px;
  border-color: aqua;
  outline: none;
}

/* @media screen and (max-width: 479px) {
  .app {
    margin: 0 5vw;
  }
} */
@media screen and (max-width: 479px) {
  .container {
    margin: 0 5vw;
  }

  /* .lets {
    display: none;
  } */

  .subtitle {
    font-size: 25px;
  }

  .maintitle {
    font-size: 100px;
  }

  .btn-open {
    width: 140px;
    padding: 0;
  }
}
</style>
