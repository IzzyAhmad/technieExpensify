<template>
  <div style="height: 100px; width 100px">
    <div class="g-signin2" data-onsuccess="onSignIn"></div>
  </div>
</template>

<script>
const axios = require("axios");
const _ = require("lodash");
//  your spreadsheet has to be PUBLIC and SHARED with everybody to be accessed this way
//  https://sheets.googleapis.com/v4/spreadsheets/{SPREASHEET_ID}/values/{SHEET_TAB_NAME}!{CELLS}?key={GOOGLE_API_KEY}
const url =
  "https://sheets.googleapis.com/v4/spreadsheets/1rc0bQCTMy4rWqI24T-HJcYT7J8gIy7kbKhBIsZDuGus/values/articles!A1:D1000?key=AIzaSyBCL9IShJzo5MrEojaYHbfD1SlGPw13dJo";

export default {
  async asyncData() {
    const response = await axios.get(url);
    console.log("this: " + response);
    const rows = response.data.values;
    const properties = rows.shift();
    const articles = [];
    for (const i in rows) {
      articles.push(_.zipObject(properties, rows[i]));
    }
    console.log("this: " + articles);
    return { articles };
  }
};
</script>

<style>
</style>