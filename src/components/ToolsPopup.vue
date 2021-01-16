<template>
  <ul id="tools" class="tools">
    <li @click="changeTextStyle('bold', null)">
      <button class="fas fa-bold"></button>
    </li>
    <li @click="changeTextStyle('formatBlock', 'h4')">
      <button class="fas fa-heading"></button>
    </li>
    <li @click="changeTextStyle('strikeThrough', null)">
      <button class="fas fa-strikethrough"></button>
    </li>
    <li @click="changeTextStyle('italic', null)">
      <button class="fas fa-italic"></button>
    </li>
    <li @click="changeTextStyle('underline', null)">
      <button class="fas fa-underline"></button>
    </li>
    <li @click="changeTextStyle('insertUnorderedList', null)">
      <button class="fas fa-list-ul"></button>
    </li>
    <li @click="addLink">
      <button class="fas fa-link"></button>
    </li>
    <li @click="changeTextStyle('unlink', null)">
      <button class="fas fa-unlink"></button>
    </li>
    <li @click="changeTextStyle('hiliteColor', 'khaki')">
      <button class="fas fa-highlighter"></button>
    </li>
  </ul>
</template>

<script>
export default {
  components: {},
  methods: {
    addLink() {
      const linkURL = prompt("Enter a URL:", "http://");

      if (linkURL != null) {
        document.execCommand("createlink", false, linkURL);
        const links = document.querySelector("#content-ul");
        const aLinks = Array.prototype.slice.call(links.querySelectorAll("a"));
        aLinks.forEach(function (link) {
          link.addEventListener("click", function () {
            if (link.href && link.href != "") {
              window.open(link.href, "_blank");
            }
          });
        });
      }
      const element = document.getElementById("tools");
      element.style.display = "none";
    },
    makeEditableAndHighlight(styleType, optParam) {
      if (typeof optParam == "undefined" || optParam == null) {
        optParam = null;
      }

      let { range, sel } = window.getSelection();

      if (sel && sel.rangeCount && sel.getRangeAt) {
        range = sel.getRangeAt(0);
      }
      document.designMode = "on";
      if (range) {
        sel.removeAllRanges();
        sel.addRange(range);
      }
      // Use HiliteColor since some browsers apply BackColor to the whole block
      /*if (!document.execCommand("HiliteColor", false, colour)) {
            document.execCommand("BackColor", false, colour);
        }*/
      document.execCommand(styleType, false, optParam);
      document.designMode = "off";
    },
    changeTextStyle(styleType, optParam) {
      if (typeof optParam == "undefined" || optParam == null) {
        optParam = null;
      }
      if (window.getSelection) {
        // IE9 and non-IE
        try {
          if (!document.execCommand(styleType, false, optParam)) {
            this.makeEditableAndHighlight(styleType, optParam);
          }
        } catch (ex) {
          this.makeEditableAndHighlight(styleType, optParam);
        }
      } else if (document.selection && document.selection.createRange) {
        // IE <= 8 case
        const range = document.selection.createRange();
        range.execCommand(styleType, false, optParam);
        //range.execCommand("BackColor", false, colour);
      }
      const element = document.getElementById("tools");
      element.style.display = "none";
    },
  },
  created() {
    let x;
    let type;
    if (!window.x) {
      x = {};
    }

    x.Selector = {};
    x.Selector.getSelected = function () {
      var t = "";
      if (window.getSelection) {
        t = window.getSelection();
      } else if (document.getSelection) {
        t = document.getSelection();
      } else if (document.selection) {
        t = document.selection.createRange().text;
      }

      if (t && t.anchorNode && t.anchorNode.nodeType) {
        type = t.anchorNode.nodeType;
      }

      return t;
    };

    let pageX;
    let pageY;

    document.addEventListener("mouseup", function () {
      const selectedText = x.Selector.getSelected();
      const element = document.getElementById("tools");
      if (selectedText != "" && type == 3) {
        element.style.left = pageX - 250 + "px";
        element.style.top = pageY - 90 + "px";
        element.style.display = "block";
      } else {
        const active = document.getElementsByClassName("modal__dialog active");
        if (active.length == 0) {
          element.style.display = "none";
        }
      }
    });
    document.addEventListener("mousedown", function (e) {
      pageX = e.pageX;
      pageY = e.pageY;
    });
  },
};
</script>

<style scoped>
ul.tools {
  display: none;
  list-style: none;
  position: absolute;
  padding-left: 25px;
  background: #f5f7fa;
  border-radius: 5px;
  border: solid 1px khaki;
  box-shadow: 0 0 2rem -1rem rgba(0, 0, 0, 0.4);
}
ul.tools li {
  display: inline-block;
  width: 30px;
  height: 30px;
  margin-right: 25px;
  margin-bottom: 15px;
  margin-top: 15px;
  text-align: center;
}

ul.tools li button {
  border: none;
  border: solid 1px khaki;
  background: #f5f7fa;
  color: #435b71;
  height: 100%;
  width: 100%;
  cursor: pointer;
  border-radius: 5px;
}

ul.tools li button:hover {
  background: #fff;
}
</style>