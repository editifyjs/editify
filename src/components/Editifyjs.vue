<template>
  <div id="editify" class="editify">
    <h1 class="heading" v-html="heading"></h1>
    <div class="card">
      <div class="multi-button">
        <button class="fas fa-cloud-download-alt"></button>
        <button class="fas fa-share-alt"></button>
        <button class="fas fa-copy"></button>
        <button class="fas fa-save"></button>
      </div>
      <div class="container">
        <ul class="fa-ul content" id="content-ul">
          <li v-for="(item, i) in blocks" :key="i" class="list">
            <ToolsExisting
              v-if="!readonly"
              class="icon"
              style="z-index: 7"
              :index="i"
              :themeP="item.theme"
              :modeP="item.mode"
              @del="del"
              @change="change"
              @setCode="setCode"
            />
            <p
              v-if="item.type == 'text'"
              :class="{ readonly: !readonly }"
              class="editable like-pre"
              v-html="item.content"
              @keyup.ctrl.enter="onInput($event, i)"
            ></p>
            <div
              v-else-if="item.type == 'code'"
              style="z-index: 1; padding-top: 6px"
            >
              <vue-codeditor
                v-model="item.content"
                :mode="item.code"
                :theme="item.theme"
                :readonly="String(readonly)"
              />
            </div>
            <div
              v-else-if="item.type == 'blockquote'"
              style="z-index: 1; padding-top: 10px"
            >
              <blockquote
                :class="{ readonly: !readonly }"
                class="editable like-pre"
                v-html="item.content"
                @keyup.ctrl.enter="onInput($event, i)"
              ></blockquote>
            </div>
          </li>
          <li class="list" v-if="!readonly">
            <ToolsNew
              class="icon"
              style="z-index: 7"
              :themeP="block.theme"
              :modeP="block.mode"
              @changeNew="changeNew"
              @setCodeNew="setCodeNew"
            />
            <p
              v-if="block.type == 'text'"
              class="editable like-pre readonly"
              v-html="block.content"
              @keyup.ctrl.enter="add($event, 'text')"
            ></p>
            <div
              v-else-if="block.type == 'code'"
              style="z-index: 1; padding-top: 6px"
              @keyup.ctrl.enter="add($event, 'code')"
            >
              <vue-codeditor
                v-model="block.content"
                :mode="block.mode"
                :theme="block.theme"
              />
            </div>
            <div
              v-else-if="block.type == 'blockquote'"
              style="z-index: 1; padding-top: 10px"
            >
              <blockquote
                class="editable like-pre readonly"
                v-html="block.content"
                @keyup.ctrl.enter="add($event, 'blockquotes')"
              ></blockquote>
            </div>
          </li>
        </ul>
      </div>
    </div>
    <ToolsPopup v-if="!readonly" style="z-index: 7" />
  </div>
</template>

<script>
import VueCodeditor from "vue-codeditor";
import ToolsPopup from "./ToolsPopup";
import ToolsNew from "./ToolsNew";
import ToolsExisting from "./ToolsExisting.vue";

export default {
  components: {
    ToolsPopup,
    VueCodeditor,
    ToolsNew,
    ToolsExisting,
  },
  props: ["blocks", "readonly", "heading"],
  data() {
    return {
      block: {
        type: "text",
        content: "",
        theme: "monokai",
        mode: "javascript",
      },
    };
  },
  methods: {
    add(e, type) {
      if (type != "code") {
        this.block.content = e.target.innerHTML;
      }

      this.blocks.push({
        type: this.block.type,
        content: this.block.content,
        mode: this.block.mode,
        theme: this.block.theme,
      });

      this.block.type = "text";
      this.block.content = "";
    },
    onInput(e, index) {
      this.blocks[index].content = e.target.innerHTML;
    },
    change(index, type) {
      this.blocks[index].type = type;
      if (type == "code") {
        this.blocks[index].content = "";
      }
    },
    del(index) {
      this.blocks.splice(index, 1);
    },
    changeNew(type) {
      this.block.type = type;
      if (type == "code") {
        this.block.content = "";
      }
    },
    setCode(theme, mode, index) {
      this.blocks[index].theme = theme;
      this.blocks[index].mode = mode;
    },
    setCodeNew(theme, mode) {
      this.block.theme = theme;
      this.block.mode = mode;
    },
  },
};
</script>

<style scoped>
.heading {
  text-align: center;
  margin-bottom: 5%;
  font-weight: 500;
}
.editify {
  display: grid;
  padding: 11%;
  background: #f5f7fa;
  font-family: Verdana, Geneva, sans-serif;
  font-size: 16px;
  letter-spacing: 1.6px;
  word-spacing: 1.8px;
  font-weight: 400;
  text-decoration: none;
  font-style: normal;
  font-variant: normal;
  text-transform: none;
  color: #435b71;
  min-height: 10em;
  position: relative;
}

.card {
  --background: #fff;
  --text: #435b71;
  position: relative;
  height: auto;
  box-shadow: 0 0 2rem -1rem rgba(0, 0, 0, 0.05);
}

.card .container {
  width: 100%;
  height: auto;
  border-radius: 1rem;
  background: var(--background);
  color: var(--text);
  padding: 7% 12% 2% 5%;
  border: 2px solid #f5f7fa;
  position: relative;
}

.card .multi-button {
  z-index: 0;
  position: absolute;
  top: 1.25rem;
  left: 1.25rem;
  border-radius: 100%;
  width: 0rem;
  height: 0rem;
  transform: translate(-50%, -50%);
  transition: 0.25s cubic-bezier(0.25, 0, 0, 1);
}

.card .multi-button button {
  display: grid;
  place-items: center;
  position: absolute;
  width: 2rem;
  height: 2rem;
  border: 1px solid khaki;
  border-radius: 100%;
  background: var(--background);
  color: var(--text);
  transform: translate(-50%, -50%);
  cursor: pointer;
  transition: 0.25s cubic-bezier(0.25, 0, 0, 1);
  box-shadow: 0 0 0rem -0.25rem var(--background);
}

.card .multi-button button:hover {
  background: var(--text);
  color: var(--background);
  box-shadow: 0 0 1rem -0.25rem var(--background);
}

.card .multi-button button:first-child:nth-last-child(1):nth-child(1),
.card .multi-button button:first-child:nth-last-child(1) ~ *:nth-child(1) {
  left: 25%;
  top: 25%;
}

.card .multi-button button:first-child:nth-last-child(2):nth-child(1),
.card .multi-button button:first-child:nth-last-child(2) ~ *:nth-child(1) {
  left: 37.5%;
  top: 18.75%;
}

.card .multi-button button:first-child:nth-last-child(2):nth-child(2),
.card .multi-button button:first-child:nth-last-child(2) ~ *:nth-child(2) {
  left: 18.75%;
  top: 37.5%;
}

.card .multi-button button:first-child:nth-last-child(3):nth-child(1),
.card .multi-button button:first-child:nth-last-child(3) ~ *:nth-child(1) {
  left: 50%;
  top: 15.625%;
}

.card .multi-button button:first-child:nth-last-child(3):nth-child(2),
.card .multi-button button:first-child:nth-last-child(3) ~ *:nth-child(2) {
  left: 25%;
  top: 25%;
}

.card .multi-button button:first-child:nth-last-child(3):nth-child(3),
.card .multi-button button:first-child:nth-last-child(3) ~ *:nth-child(3) {
  left: 15.625%;
  top: 50%;
}

.card .multi-button button:first-child:nth-last-child(4):nth-child(1),
.card .multi-button button:first-child:nth-last-child(4) ~ *:nth-child(1) {
  left: 62.5%;
  top: 18.75%;
}

.card .multi-button button:first-child:nth-last-child(4):nth-child(2),
.card .multi-button button:first-child:nth-last-child(4) ~ *:nth-child(2) {
  left: 37.5%;
  top: 18.75%;
}

.card .multi-button button:first-child:nth-last-child(4):nth-child(3),
.card .multi-button button:first-child:nth-last-child(4) ~ *:nth-child(3) {
  left: 18.75%;
  top: 37.5%;
}

.card .multi-button button:first-child:nth-last-child(4):nth-child(4),
.card .multi-button button:first-child:nth-last-child(4) ~ *:nth-child(4) {
  left: 18.75%;
  top: 62.5%;
}

.card:hover .multi-button,
.card .multi-button:focus-within {
  width: 10rem;
  height: 10rem;
}

.readonly {
  -webkit-user-modify: read-write;
}

.editable {
  outline: none;
  box-sizing: border-box;
  word-wrap: break-word;
  line-break: after-white-space;
  -webkit-line-break: after-white-space;
}

.like-pre {
  display: block; /* inline-block */
  unicode-bidi: embed;
  white-space: pre;
  white-space: pre-wrap; /* Since CSS 2.1 */
  white-space: -moz-pre-wrap; /* Mozilla, since 1999 */
  white-space: -pre-wrap; /* Opera 4-6 */
  white-space: -o-pre-wrap; /* Opera 7 */
  word-wrap: break-word; /* Internet Explorer 5.5+ */
  background-color: transparent;
}

.icon {
  margin-top: 2px;
  cursor: pointer;
  display: none;
  color: #435b71;
}

.list {
  margin-bottom: 25px;
}

.list:hover .icon {
  display: block;
}

blockquote {
  display: inline;
  background: #f9f9f9;
  border-left: 8px solid #ccc;
  margin-top: -5px;
  padding: 0.5em 10px;
  quotes: "\201C""\201D""\2018""\2019";
  margin-left: -0.5px;
}

blockquote:before {
  color: #ccc;
  content: open-quote;
  font-size: 2em;
  line-height: 0.1em;
  margin-right: 0.25em;
  vertical-align: -0.4em;
}

blockquote:after {
  color: #ccc;
  content: close-quote;
  font-size: 2em;
  line-height: 0.1em;
  margin-left: 0.25em;
  vertical-align: -0.4em;
}
</style>