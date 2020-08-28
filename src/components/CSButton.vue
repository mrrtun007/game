<template>
<div>
  
    <div class="row text-light">
      <div class="col-sm">
        <p>{{randomPlayer}}</p>
        <p>HP : {{hp1}}</p>
        <p>
          <img v-bind:style="{width : hp1 + 'px'}" :src="healthbar" alt height="60px" />
        </p>
        <img :src="imagePlayer" :height="hp1" />
      </div>

      <div class="col-sm text-danger">
        <h1 v-if="hp1 <= 0 & hp2 <=0">
          <br />
          <img src="https://image.freepik.com/free-vector/you-win-sign-pop-art-style_175838-498.jpg">
          DRAW!
          
        </h1>
        <h1 v-else-if="hp2 <= 0 ">
          <br />
          <img src="https://media2.giphy.com/media/2gtoSIzdrSMFO/giphy.gif">
          {{randomPlayer}} WIN
        </h1>
        <h1 v-else-if="hp1 <= 0 ">
          <br />
          <img src="https://media2.giphy.com/media/2gtoSIzdrSMFO/giphy.gif">
          {{randomMonster}} WIN
        </h1>
        <br /><br /><br />
        <p v-if="hp1!=0 & hp2!=0">
  
        </p>
      </div>
      <div class="col-sm">
        <p>{{randomMonster}}</p>
        <p>HP : {{hp2}}</p>
        <p>
          <img v-bind:style="{width: hp2 + 'px'}" :src="healthbar" alt height="60px" />
        </p>
        <img :src="imageMonster" :height="hp2" />
      </div>
    </div>
    <v-button @click="randomStart()" class="btn">
    <img src="https://cdn.discordapp.com/attachments/392353546332405763/747437885476700160/pngegg_11.png"/>
    </v-button>
    <br />
    <button v-bind:disabled="end" @click="randomDamage()" class="btn btn-info">
    Attack{{Label}}</button>
    <button v-bind:disabled="end" @click="randomSpDamage()" @click.prevent="playSound(player[chosenNumber1].spsound)"  class="btn btn-info">
      Special Attack{{Label}}</button>
  </div>



</template>

<script>
export default {
  data: function () {
    return {
      randomPlayer: "",
      randomMonster: "",
      randomPlayerAttack: "",
      randomMonsterAttack: "",
      chosenNumber1:"",
      chosenNumber2:"",
      imagePlayer: "",
      imageMonster: "",
      hp1: "1",
      hp2: "1",
      end: true,
      healthbar:
           "https://i.ppy.sh/bca61e3c2183a86ddb4c1d75914fab845e2b128f/687474703a2f2f692e696d6775722e636f6d2f6953766c5662432e706e67",
      audios: [
      {
        file: new Audio('https://cdn.discordapp.com/attachments/392353546332405763/748765378167046204/KId6eunoiWk.mp3'),
        isPlaying: false
      }],
        player: [
        {
          name: "Naruto",
          hp: 380,
          image1:
            "https://giffiles.alphacoders.com/209/209863.gif",
          image2:
            "https://giffiles.alphacoders.com/207/207987.gif",
          image3:
            "https://avatarfiles.alphacoders.com/106/10638.gif",
   
        },
        {
          name: "Monkey D. Luffy",
          hp: 360,
          image1:
            "https://avatars.alphacoders.com/avatars/view/125919",
          image2:
            "https://avatars.alphacoders.com/avatars/view/125919",
          image3:
            "https://avatars.alphacoders.com/avatars/view/125919",

        },
        {
          name: "Goku",
          hp: 350,
          image1:
            "https://pa1.narvii.com/6405/92030e6558d220e1892c435e82e0684a500b5b6c_hq.gif",
          image2:
            "https://pa1.narvii.com/6405/74658f74d77a16a5dd2cb6b267826dbbdc531339_hq.gif",
          image3:
            "https://giffiles.alphacoders.com/350/35060.gif",
  
        },
      ],
      monster: [
        {
          name: "Roronoa Zoro",
          hp: 430,
          image1:
            "https://avatarfiles.alphacoders.com/132/132683.png",
          image2:
            "https://avatars.alphacoders.com/avatars/view/10691",
        },
        {
          name: "Trafalgar Law",
          hp: 420,
          image1:
            "https://avatarfiles.alphacoders.com/169/169159.jpg",
          image2:
            "hhttps://avatarfiles.alphacoders.com/169/169159.jpg",
        },
        {
          name: "Brook",
          hp: 400,
          image1:
            "https://avatarfiles.alphacoders.com/116/116667.jpg",
          image2:
            "https://avatarfiles.alphacoders.com/116/116667.jpg",
        },
      ],
    };
  },
  props: {
    Label: String,
  },

  methods: {
    randomStart: function () {
      this.chosenNumber1 = Math.floor(Math.random() * this.player.length);
      this.randomPlayer = this.player[this.chosenNumber1].name;
      this.hp1 = this.player[this.chosenNumber1].hp;
      this.imagePlayer = this.player[this.chosenNumber1].image1;
      this.chosenNumber2 = Math.floor(Math.random() * this.monster.length);
      this.randomMonster = this.monster[this.chosenNumber2].name;
      this.hp2 = this.monster[this.chosenNumber2].hp;
      this.imageMonster = this.monster[this.chosenNumber2].image1;
      this.end = false;
    },
    randomDamage: function () {
      this.randomPlayerAttack = Math.max(Math.floor(Math.random() * 10) + 1, 3);
      this.hp2 -= this.randomPlayerAttack;
      this.imagePlayer = this.player[this.chosenNumber1].image2;      
      this.randomMonsterAttack = Math.max(Math.floor(Math.random() * 15) + 1,5);
      this.hp1 -= this.randomMonsterAttack;
      this.imageMonster = this.monster[this.chosenNumber2].image2;
      if (this.hp1 <= 0 & this.hp2 <=0) {
        this.hp1 = 0;
        this.hp2 = 0;
        this.end = true;        
      }
      else if (this.hp1 <= 0) {
        this.hp1 = 0;
        this.end = true;
        this.imageMonster = this.monster[this.chosenNumber2].image1;
      }
      else if (this.hp2 <= 0) {
        this.hp2 = 0;
        this.end = true;
        this.imagePlayer = this.player[this.chosenNumber1].image1;
      }
    },
    randomSpDamage: function () {
      this.randomPlayerAttack = Math.max(Math.floor(Math.random() * 20) + 1,10);
      this.hp2 -= this.randomPlayerAttack;
      this.imagePlayer = this.player[this.chosenNumber1].image3;      
      this.randomMonsterAttack = Math.max(Math.floor(Math.random() * 15) + 1,5);
      this.hp1 -= this.randomMonsterAttack;
      this.imageMonster = this.monster[this.chosenNumber2].image2;    
      if (this.hp1 <= 0 & this.hp2 <=0) {
        this.hp1 = 0;
        this.hp2 = 0;
        this.end = true;             
      }
      else if (this.hp1 <= 0) {
        this.hp1 = 0;
        this.end = true;
        this.imageMonster = this.monster[this.chosenNumber2].image1
      }
      else if (this.hp2 <= 0) {
        this.hp2 = 0;
        this.end = true;
        this.imagePlayer = this.player[this.chosenNumber1].image1;
      }
    },
    playSound (sound) {
      if(sound) {
        var audio = new Audio(sound);
        audio.play();
      }
    },
    play (audio) {
      audio.isPlaying = true;
      audio.file.play();
    },
    pause (audio) {
      audio.isPlaying = false;
      audio.file.pause();
    }
  },
};
</script>

<style>
</style>