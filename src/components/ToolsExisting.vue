<template>
  <!-- The dropdown -->
  <div class="dropdown">
    <button class="fa-li icon dropbtn">
      <i class="fas fa-grip-vertical"></i>
    </button>
    <!-- The dropdown-content -->
    <div class="dropdown-content">
      <a @click="change('text')"
        ><i class="fas fa-text-width"></i
        ><span>Text<small>Convert</small></span></a
      >
      <a @click="change('blockquote')"
        ><i class="fas fa-quote-left"></i
        ><span>Quote<small>Convert</small></span></a
      >
      <a @click="active = !active"
        ><i class="fas fa-code"></i><span>Code<small>Convert</small></span></a
      >
      <!-- The modal -->
      <div class="modal" id="linkModal">
        <!-- The modal dialog -->
        <div class="modal__dialog" :class="{ active: active }">
          <div class="modal__content">
            <button class="modal__close" @click="active = !active">
              <i class="fa fa-times"></i>
            </button>
            <div class="modal__body">
              <select v-model="theme" name="themes">
                <option v-for="(item, i) in themes" :key="i" :value="item">
                  {{ item }}
                </option>
              </select>
              <select v-model="mode" name="modes">
                <option v-for="(item, i) in modes" :key="i" :value="item">
                  {{ item }}
                </option>
              </select>
            </div>
            <div class="modal__footer">
              <button class="button" @click="setCode('code')">Complate</button>
            </div>
          </div>
        </div>

        <!-- The overlay for the modal -->
        <div class="modal__overlay"></div>
      </div>
      <a @click="del"><i class="fas fa-trash-alt"></i><span>Delete</span></a>
    </div>
  </div>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      active: false,
      modeNew: "",
      themeNew: "",
      themes: [
        "monokai",
        "chrome",
        "dracula",
        "eclipse",
        "github",
        "cobalt",
        "terminal",
        "twilight",
        "xcode",
      ],
      modes: [
        "javascript",
        "java",
        "python",
        "html",
        "css",
        "golang",
        "sql",
        "csharp",
        "gherkin",
        "haml",
        "json",
        "php",
        "ruby",
        "scala",
        "sass",
        "swift",
        "typescript",
        "xml",
        "yaml",
      ],
    };
  },
  props: ["index", "modeP", "themeP"],
  computed: {
    mode: {
      // getter
      get() {
        return this.modeP;
      },
      set(newValue) {
        this.modeNew = newValue;
      },
    },
    theme: {
      // getter
      get() {
        return this.themeP;
      },
      set(newValue) {
        this.themeNew = newValue;
      },
    },
  },
  methods: {
    change(type) {
      this.$emit("change", this.index, type);
    },
    del() {
      this.$emit("del", this.index);
    },
    setCode(type) {
      this.$emit(
        "setCode",
        this.themeNew ? this.themeNew : this.themeP,
        this.modeNew ? this.modeNew : this.modeP,
        this.index
      );
      this.active = !this.active;
      this.change(type);
    },
  },
};
</script>

<style scoped>
.dropdown {
  position: relative;
  display: inline-block;
}

.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f5f7fa;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  z-index: 1;
}

.dropdown-content a {
  padding: 12px 16px;
  text-decoration: none;
  display: block;
  font-family: Verdana, Geneva, sans-serif;
  font-size: 14px;
  letter-spacing: 0.8px;
  word-spacing: 1.8px;
  font-weight: 400;
  text-decoration: none;
  font-style: normal;
  font-variant: normal;
  text-transform: none;
  color: #435b71;
}

.dropdown-content a:hover {
  background-color: white;
}

.dropdown-content a span {
  margin-left: 15px;
}

.dropdown-content a span small {
  margin-left: 10px;
  font-size: 8px;
  border: 1px solid khaki;
  padding: 3px;
  border-radius: 5px;
}

.dropdown-content a i {
  padding: 5px;
  border-radius: 5px;
  border: solid 1px khaki;
  width: 35px;
  text-align: center;
}

.dropdown:hover .dropdown-content {
  display: block;
}

.dropdown .dropbtn {
  background: none;
  border: none;
  cursor: pointer;
  color: #435b71;
}

.dropdown:hover .dropbtn {
  background-color: #f5f7fa;
  border-radius: 5px;
  border: solid 1px khaki;
  cursor: pointer;
  color: #435b71;
}

select {
  border: 1px solid rgba(0, 0, 0, 0.1);
  background: #ffffff;
  box-shadow: none;
  color: #000;
  padding: 16px;
  outline: 0;
  margin: 0 auto;
  margin-bottom: 15px;
  font-weight: 300;
  font-size: 11px;
  letter-spacing: 1px;
  cursor: pointer;
  border-radius: 5px;
  width: 88%;
}

select::placeholder {
  color: #c9c9c9;
  font-size: 11px;
}

select:focus {
  color: #555555;
  background: #ffffff;
  border-color: khaki;
}

.button {
  cursor: pointer;
  background: #435b71;
  border: 0;
  border-radius: 5px;
  color: #ffffff;
  padding: 12px 60px;
  font-weight: 700;
  font-size: 15px;
  outline: 0;
  text-transform: uppercase;
  margin: 0 auto;
  display: table;
  width: 60%;
}

.button:hover {
  background: #ffffff;
  color: #435b71;
  border: 1px solid #435b71;
  border-radius: 5px;
}

.modal {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.modal__cta {
  margin: 24px 0;
  font-size: 24px;
  color: rgba(0, 0, 0, 0.45);
}

.modal__overlay {
  position: fixed;
  width: 100%;
  height: 100%;
  visibility: hidden;
  top: 0;
  left: 0;
  z-index: 1000;
  opacity: 0;
  background: white;
  transition: all 0.25s;
}

.modal__dialog {
  position: fixed;
  top: 50%;
  left: 50%;
  width: 50%;
  max-width: 630px;
  min-width: 320px;
  height: auto;
  z-index: 2000;
  visibility: hidden;
  backface-visibility: hidden;
  transform: translateX(-50%) translateY(-50%);
  perspective: 1300px;
}

.modal__dialog.active {
  opacity: 1;
  visibility: visible;
}

.modal__dialog.active ~ .modal__overlay {
  opacity: 0.9;
  visibility: visible;
}

.modal__dialog.active .modal__content {
  transform: rotateX(0deg);
  opacity: 1;
}

.modal__content {
  background: #fafafa;
  border-radius: 2px;
  padding: 24px;
  color: #131313;
  position: relative;
  transform-style: preserve-3d;
  transform: rotateX(-60deg);
  transform-origin: 50% 0;
  opacity: 0;
  transition: all 0.25s;
}

.modal__close {
  position: absolute;
  right: -14px;
  top: -16px;
  color: #fff;
  background: #435b71;
  border: 0;
  outline: 0;
  border-radius: 50%;
  font-size: 16px;
  width: 32px;
  height: 32px;
  cursor: pointer;
}

.modal__header {
  text-align: center;
  font-weight: 300;
  font-size: 24px;
  color: rgba(0, 0, 0, 0.45);
}

.modal__body {
  color: #ffffff;
  display: flex;
  margin: 0 auto;
  width: 100%;
  max-width: 400px;
  flex-direction: column;
}

.modal__footer {
  margin: 24px 0;
}
</style>