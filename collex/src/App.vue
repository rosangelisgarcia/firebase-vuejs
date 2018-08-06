<template>
  <div id="app">
    <div v-for="item in items" :key="item.id">
      <img v-bind:src="imgpath(item)" alt="">
      <a v-bind:href="item.pageurl" target="_blank">
        <h1>{{ item.title }}</h1>
        <h2>{{ item.author }}</h2>
      </a>
    </div>
  </div>
</template>

<script>
var catid = parseInt(window.location.href.split("=").pop());
import Firebase from 'firebase'
let config = {
  apiKey: "",
  authDomain: "",
  databaseURL: "",
  projectId: "",
  storageBucket: "",
  messagingSenderId: ""
}
let app = Firebase.initializeApp(config);
let db = app.database();
let itemsRef = db.ref("items");

export default {
  name: 'app',
  firebase: {
    //items: itemsRef
    items: itemsRef.orderByChild('categoryid').equalTo(catid)
  },
  methods: {
    imgpath: function(i){
      return "/static/images/" + i.imgname + ".jpg";
    }
  }
}
</script>

<style scoped>
#app {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  padding: 10px 0 60px 0;
}

#app div {
  width: 300px;
  height: 185px;
  border: solid 1px gray;
  border-radius: 2px;
  margin: 0.5em;
  box-shadow: 2px 2px 2px silver;
  position: relative;
}

#app div img {
  position: absolute;
  display: block;
  width: 100%;
  height: 100%;
  z-index: 10;
}

#app div h1 {
  position: absolute;
  z-index: 15;
  margin: 0;
  top: 0;
  left: 8px;
  font-size: 18px;
}

#app div h2 {
  position: absolute;
  z-index: 15;
  margin: 0;
  top: 18px;
  left: 8px;
  font-size: 16px;
}

#app div a {
  display: block;
  position: absolute;
  z-index: 20;
  background:linear-gradient(gray, transparent);
  width: 100%;
  height: 100%;
  color: white;
  text-shadow: 1px 1px gray;
}
</style>
