<template>
  <v-app class="app" style="background: #f5f7fa; color: #435b71">
    <Header />
    <Editifyjs
      :blocks="blocks"
      heading="Modern Vue.js editor &#127942;&#127881;"
    />
    <h2>Editor Output &#127917;</h2>
    <div class="container">
      heading: "Modern Vue.js editor &#127942;&#127881;", <br />
      blocks: [
      <div v-for="(item, i) in blocks" :key="i">
        <pre v-if="item.type != 'code'">
          &nbsp;&nbsp; { <br />
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; type: "{{item.type}}", <br />
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; content: "{{item.content}}", <br />
          &nbsp;&nbsp; }, 
        </pre>
      </div>

      ], <br />
      time: " {{ new Date() }}"
    </div>
    <h2>Bugs and features that continue to develop &#128373;🛠️</h2>
    <v-container class="container">
      <Features />
    </v-container>
    <h2>Write us for your suggestions and comments &#9997;&#10024;</h2>
    <v-container class="container">
      <Comments />
    </v-container>
    <Footer />
  </v-app>
</template>

<script>
import Header from "./components/Header";
import Editifyjs from "./components/Editifyjs";
import Features from "./components/Features";
import Comments from "./components/Comments";
import Footer from "./components/Footer";

export default {
  name: "App",

  components: {
    Header,
    Editifyjs,
    Features,
    Comments,
    Footer,
  },

  data: () => ({
    blocks: [
      {
        type: "text",
        content:
          '<span style="background-color: khaki;">Modern</span>, block-style, completely free (MIT license) and <span style="background-color: khaki;">pioneering</span> Vue editor!',
        theme: "monokai",
        mode: "javascript",
      },
      {
        type: "text",
        content:
          "This editor component, which you can use in your vue js projects as you wish, includes many <u>features</u>:",
        theme: "monokai",
        mode: "javascript",
      },
      {
        type: "text",
        content:
          '<ul><li>Editable and developable text feature,</li><li>And blockqute feature for your articles that you want to use with quotes or highlight,<br></li><li>One of the most important features is the advanced level code editor, click <a href="https://github.com/oclk/vue-codeditor" target="_blank">here</a> for detailed code editor information,<br></li><li>and more...<br></li></ul>',
        theme: "monokai",
        mode: "javascript",
      },
      {
        type: "blockquote",
        content:
          '"The better we get at getting better, the faster we will get better." - <b><i>Douglas</i> </b><i><b>Engelbart</b></i>',
        theme: "monokai",
        mode: "javascript",
      },
      {
        type: "text",
        content:
          "Now let's examine the <strike>algorithms</strike> with different programming languages to explore the code editor features",
        theme: "monokai",
        mode: "javascript",
      },
      {
        type: "text",
        content:
          'Start with <b><span style="background-color: khaki;">javascript</span> </b>first:',
        theme: "monokai",
        mode: "javascript",
      },
      {
        type: "code",
        content:
          "function bubble_Sort(a)\n{\n\tvar swapp;\n\tvar n = a.length-1;\n\tvar x=a;\n\tdo {\n\t\tswapp = false;\n\t\tfor (var i=0; i < n; i++)\n\t\t{\n\t\t\tif (x[i] < x[i+1])\n\t\t\t{\n\t\t\t\tvar temp = x[i];\n\t\t\t\tx[i] = x[i+1];\n\t\t\t\tx[i+1] = temp;\n\t\t\t\tswapp = true;\n\t\t\t}\n\t\t}\n\t\tn--;\n\t} while (swapp);\n\treturn x; \n}\n\nconsole.log(bubble_Sort([12, 345, 4, 546, 122, 84, 98, 64, 9, 1, 3223, 455, 23, 234, 213]));",
        theme: "chrome",
        mode: "javascript",
      },
      {
        type: "text",
        content:
          'Continue with the <b><span style="background-color: khaki;">Json</span></b>:',
        theme: "monokai",
        mode: "javascript",
      },
      {
        type: "code",
        content:
          '{\n\t"name" : "Admin",\n\t"age" : 36,\n\t"rights" : [ "admin", "editor", "contributor" ]\n}',
        theme: "dracula",
        mode: "json",
      },
      {
        type: "blockquote",
        content:
          "And <i>code editor</i> can be used with many <u>other</u> programming languages...",
        theme: "monokai",
        mode: "javascript",
      },
      {
        type: "text",
        content:
          'Finally, by pressing <span style="background-color: khaki;">ctrl/enter</span>, a new item can be <b>dynamically</b> added to the list or you can save changes on the item!',
        theme: "monokai",
        mode: "javascript",
      },
    ],
  }),
};
</script>


<style scoped>
.container {
  height: auto;
  border-radius: 1rem;
  color: #435b71;
  padding: 4% 4% 4% 4%;
  border: 1px solid #435b71;
  overflow-x: auto;
  overflow-y: hidden;
  white-space: nowrap;
  margin-bottom: 100px;
}

h2 {
  font-weight: 200;
  margin-left: 12%;
  margin-bottom: 1%;
}
</style>