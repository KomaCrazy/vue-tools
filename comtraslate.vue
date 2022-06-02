<template>
  <div>
    <div class="container">
      <h3>Translate</h3>

    <textarea id="input1" rows="10" cols="50" v-model="text1" v-on:input="convert()"></textarea>
    <textarea id="output1" rows="10" cols="50"></textarea>
    </div>

</div>
</template>
<script>
export default {
  name: "comtranslate",
  components: {},
  data() {
    return {
      text: "",
      text1: "",
      box1: "",
      items: [],
    };
  },
  mounted() {},
  methods: {
    translate(sentences, targetDiv, from_lang = "th", to_lang = "en") {
      sentences = sentences.replace(/\n/g, "<br>");
      let endPoint = `https://translate.googleapis.com/translate_a/single?client=gtx&sl=${from_lang}&tl=${to_lang}&dt=t&ie=UTF-8&oe=UTF-8&q=${encodeURIComponent(
        sentences
      )}`;

      var xhttp = new XMLHttpRequest();
      xhttp.onreadystatechange = function () {
        if (this.readyState == 4 && this.status == 200) {
          var jsonText = JSON.parse(this.responseText);
          this.text = jsonText[0][0][0];
          this.text = this.text.replace(/<br>/g, "\n");
          targetDiv.innerHTML = "&nbsp;" + this.text;
        }
      };
      xhttp.open("GET", endPoint, true);
      xhttp.send();
    },
    convert() {
      console.log(this.text1);
      //.innerHTML = this.text1;
      this.translate(this.text1, this.box1 = document.getElementById("output1"), this.from_lang ='en', this.to_lang='th')
    },
  },
};
</script>
