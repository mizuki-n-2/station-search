<template>
  <div class="home flex">
    <div class="home-container">
      <input type="text" v-model="stationName" placeholder="駅名を入力してください">
      <button @click="showInfo">検索</button>
      <p v-for="(data,index) in lists" :key="index">
        駅情報{{index+1}}：{{data}}
      </p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      stationName: "",
      lists: []
    };
  },
  methods: {
    async showInfo() {
      this.lists = [];
      let item = await axios.get(`//api.ekispert.jp/v1/json/station?key=LE_zmTrsNKamrkQm&name=${this.stationName}`);
      for (let i=0;i < item.data.ResultSet.Point.length;i++) {
        this.lists.push(item.data.ResultSet.Point[i].Station.Name);
      }
      // console.log(item);
      // console.log(this.lists);
    }
  }
};
</script>

<style scoped>
.flex {
  display: flex;
  justify-content: center;
}

.home-container {
  margin-top: 100px;
  background: #eee;
  padding: 30px 60px;
  border: 1px solid #000;
  border-radius: 5px;
}

.home-container p {
  margin: 20px 0;
  padding-top: 10px;
  border-bottom: 1px solid #ccc;
}
</style>
