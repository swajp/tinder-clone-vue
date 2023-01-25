<template>
  <v-app>
    <div class="background">
    <div class="container">
      <div class="container-child-left">
        <div class="header">
          <button><img src="../images/prof.jpg" alt=""></button>
          <h1 class="headertext">My profile</h1>
        </div>
        <div class="match-cards">
          <div v-on:click="selectMatch(item)" class="matched-card"  v-for="(item,index) in matches" :key="index">
              <img :src="item.img">
              <div class="lala">
                <h1 style="color: white; font-size: 16px; font-weight: 500;">{{item.name}}</h1>
              </div>
          </div>
        </div>
      </div>
      <div class="container-child-right">
        <div v-if="isHidden"> 
          <div class="main-card" v-for="item in filteredItems" :key="item.id">
            <div class="person-card">
                <img :src="item.img">
                <div class="gradient"></div>
              <div class="person-info">
                <h1>{{item.name}} <span>{{item.age}}</span></h1>
                <p style="width: 80%">{{item.description}}</p>
              </div>
            </div>
            <div class="actions">
              <button @click="swipeDislike"><div class="action"><img src="../images/dislike.svg" alt=""></div></button>
              <button @click="swipeStar"><div class="action"><img src="../images/star.svg" alt=""></div></button>
              <button @click="swipeLike"><div class="action"><img src="../images/like.svg" alt=""></div></button>
            </div>
          </div>
        </div>
      </div>
      <div v-if="!isHidden">
        <div v-for="item in clickedPerson" :key="item.id" class="main-card">
          <div style="text-align: right; margin-right: 12px; color: white;"><button v-on:click="isHidden = !isHidden"><h1>X</h1></button></div>
          <div class="person-card">
              <img :src="item.img">
              <div class="gradient"></div>
            <div class="person-info">
              <h1>{{item.name}}</h1>
            </div>
          </div>
          <div class="actions-unmatch">
            <button @click="swipeDislike"><div class="action-unmatch"><p>UNMATCH</p></div></button>
          </div>
        </div>
      </div>
    </div>
  </div>
  </v-app>
</template>

<script>  

export default {
  name: 'App',
  data() {
    return {
      items: [
        {"id": 1, "name": "Jenna Ortega", "age": "20", description: "I like to dance.", "match": 0, img: [require("../images/jennaortega.jpg"),]},
        {"id": 2, "name": "Olivia Rodrigo", "age": "19", description: "I like to sing.", "match": 1, img: [require("../images/oliviarodrigo.jpg")]},
        {"id": 3, "name": "Petr Pavel", "age": "69", description: "I like to shoot.", "match": 1, img: [require("../images/petrpavel.jpg")]},
        {"id": 4, "name": "Karel Diviš", "age": "12", description: "Volte srdcem číslo 8!.", "match": 1, img: [require("../images/kareldivis.jpg")]},
        {"id": 5, "name": "Čestmír Mázl", "age": "44", description: "Doktor na volné noze. Rád Vám budu dělat osobnío gynekologa", "match": 1, img: [require("../images/cestmirmazl.jpg")]},
        {"id": 6, "name": "Človek", "age": "9", description: "Rád žije", "match": 1, img: [require("../images/clovek.jpg")]},
        {"id": 7, "name": "Gigachad", "age": "13", description: "Svaly jsou moje hobby 💪", "match": 0, img: [require("../images/gigachad.jpg")]},
        {"id": 8, "name": "Filípek B", "age": "20", description: "velmi rad piju pojd pit semnou", "match": 1, img: [require("../images/filipek.jpg")]},
        {"id": 9, "name": "free bobux", "age": "4", description: "dam ti bobux zdarma", "match": 0, img: [require("../images/bobux.jpg")]},
        {"id": 10, "name": "the kámen", "age": "99", description: "🪨 Rock", "match": 1, img: [require("../images/rock.jpg")]},
        {"id": 11, "name": "jerremy", "age": "POWER", description: "power", "match": 1, img: [require("../images/jerremy.jpg")]},
      ],
      matches: [
        {"name": "Shrek", img: [require("../images/shrek.jpg")]},
        {"name": "Nemo", img: [require("../images/nemo.jpg")]},
      ],
      selectedId: 1,
      isHidden: true,
      selectedMatch: null,
    };
  },
  computed: {
    filteredItems() {
      return this.items.filter(item => item.id === this.selectedId);
    },
    clickedPerson() {
      return this.matches.filter(item => item.name == this.selectedMatch.name );
    },
  },
  methods: {
    swipeLike() {
      var selectedItem = this.items.find(item => item.id === this.selectedId)
      if (selectedItem.match == 1) {
        this.matches.push({name: selectedItem.name, img: selectedItem.img})
        this.selectedId++;
      }
      else {
        this.selectedId++;
      }
    },
    swipeStar() {
      var selectedItem = this.items.find(item => item.id === this.selectedId)
      if (selectedItem.match == 1) {
        this.matches.push({name: selectedItem.name, img: selectedItem.img})
        this.selectedId++;
      }
      else {
        this.selectedId++;
      }
    },
    swipeDislike() {
      this.selectedId++;
    },
    selectMatch(item) {
      this.isHidden = false;
      this.selectedMatch = item;
    }
  }
};
</script>

<style>
.background {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  overflow: auto;
  background: #202125;
}
.container-child-left {
  width: 30%;
  height: 100vh;
  float: left;
  background-color: #121212;
}  
.container-child-right {
  width: 60%;
  height: 100vh;
  float: right;
}
.header {
  background: linear-gradient(91.14deg, #FB2C7B 0%, #FF7556 100%);
  height: 8%;
  display: flex;
  justify-items: left;
  gap: 8px;
  justify-content: left;
  align-items: center;
}
.headertext{
  color: white;
  position: relative;
  font-weight: 500;
  font-size: 22px;
  margin-left: 4px;
}
.header img {
  border-radius: 30px;
  width: 56px;
  height: 56px;
  margin-left: 24px;
}
.main-card{
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(0, -50%);
}
.person-card{
  background-color: black;
  width: 500px;
  height: 750px;
  border-radius: 15px;
  box-shadow: 0px 0px 10px rgba(255, 255, 255, 0.09);
  margin-bottom: 18px;
}
.person-card img{
  width: 500px;
  height: 750px;
  position: absolute;
  border-radius: 15px;
}
.person-info{
  position: relative;
  top: 80%;
  margin-left: 16px;
  color: white;
}
.actions-unmatch{
  width: 100%;
  height: 80px;
  color: white;
  font-weight: 600;
  display: flex;
  justify-items: center;
  gap: 8px;
  justify-content: center;
}
.action-unmatch{
  cursor: pointer;
}
.actions{
  width: 100%;
  height: 80px;
  display: flex;
  justify-items: center;
  gap: 8px;
  justify-content: center;
}
.action{
  cursor: pointer;
}
.gradient{
  background: linear-gradient(180deg, rgba(255, 255, 255, 0) 58.74%, rgba(0, 0, 0, 0.9) 100%);
  width: 500px;
  height: 750px;
  position: absolute;
  border-radius: 15px;
}
span{
  font-weight: 300;
  font-size: 21px;
}
.match-cards{
  margin: 16px;
  cursor: pointer;
  flex-flow: row wrap;
  display: flex;
  justify-content: left;
  justify-items: center;
  gap: 16px;
}
.matched-card{
  width: 130px;
  height: 150px;
  background-color: rgb(27, 27, 27);
  border-radius: 15px;
}
.matched-card img{
  width: 130px;
  height: 150px;
  border-radius: 15px;
}
.lala{
  position: relative;
  top: -25%;
  margin-left: 6px;
}
</style>