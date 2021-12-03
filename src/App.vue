<template>
  <div id="app">
    <!-- Nav side -->
    <div class="w-full top">
      <svg
        class="w-full"
        xmlns="http://www.w3.org/2000/svg"
        width="1366"
        height="156"
      >
        <g fill="#63BABA" fill-rule="evenodd">
          <path
            d="M470.577 563.429c-51.432-51.425-51.438-134.806-.013-186.237l.013-.013L867.235-19.424c51.441-51.434 134.836-51.434 186.276 0 48.811 48.804 51.304 126.392 7.473 178.135l178.158-178.135c51.441-51.434 134.836-51.434 186.277 0 51.431 51.424 51.437 134.805.013 186.237-.005.004-.01.008-.013.013l-396.66 396.603c-51.44 51.433-134.834 51.433-186.275 0-48.812-48.805-51.304-126.394-7.471-178.138L656.853 563.43c-51.441 51.433-134.836 51.433-186.276 0zM342.268 45.605c-51.432-51.425-51.438-134.806-.013-186.237l.013-.013 396.658-396.603c51.441-51.434 134.836-51.434 186.277 0 51.431 51.424 51.437 134.805.013 186.237-.005.004-.01.008-.013.013L528.543 45.605c-51.44 51.433-134.834 51.433-186.275 0zm-444.692 71.824c-51.432-51.424-51.438-134.806-.013-186.237l.013-.013 396.658-396.603c51.441-51.434 134.836-51.434 186.277 0 51.431 51.424 51.437 134.805.013 186.237a80.86 80.86 0 01-.013.013L83.85 117.429c-51.44 51.433-134.834 51.433-186.275 0z"
          />
        </g>
      </svg>
    </div>
    <!-- filter input -->
    <div class="w-full flex">
      <div class="w-3/5 ml-64 h-20 filter rounded-sm flex">
      <div class="flex glob-btn " v-for="(data, i) in persSkillGot"
          :key="i">
        <span
          class="bg-green-400 rounded-xl  text-white ml-2 mr-2 text-md"
          >{{ data }}
          <!-- delete element -->
        </span>
          <button @click="supp(i)" class="bg-gray-400 rounded-xl pl-1">
            <img src="./assets/icon-remove.svg" alt="" />
          </button>

      </div>
      <button @click="clear" class='text-green-500'>Clear</button>
      </div>
    </div>
    <!-- Cards -->
    <div>
      <!-- Pour le tableau de la boucle: Quand on clique sur clear on voit le tableau de base (data) et quand on clique sur un des boutons on voit le tableau filtré (filteredCards)  -->
      <!-- Update: on ne voit que le filterCard -->
      <Card
        @getSkill="skill"
        v-for="data in filteredCards "
        :key="data.id"
        :inData="data"
      />
    </div>
  </div>
</template>

<script>
import Card from "./components/Card.vue";
import jsonDatas from "../exo-ressources/data.json";

// console.log(jsonDatas);

export default {
  name: "App",
  components: {
    Card,
  },
  data() {
    return {
      datas: jsonDatas,
      persSkillGot: [],
      index: "",
      parentEl: "",
      elemcliked: "",
      clearPressed:false,
    };
  },
  methods: {
    skill(event) {
      // this.persSkillGot = event[0];
      this.elemcliked= event
      this.persSkillGot.push(this.elemcliked);
      console.log(this.persSkillGot);
      console.log(this.elemcliked);
      // Quand on clique sur un bouton qui n'est pas clear alors il le met a false (si elemcliked n'est pas vide)
      if (this.elemcliked) {
        this.clearPressed=false
      }
    },
    supp(i) {
      //on recupere l'index de lélément sur lequel on a cliqué
      this.persSkillGot.splice(i,1)

      //si le tableau est vide il faut lancer la fonction clear
      if (this.persSkillGot.length==0) {
        this.clear();
      }
      console.log(this.persSkillGot);
      

    },
    clear() {
      this.persSkillGot=[];
      this.clearPressed=true;
      console.log(this.persSkillGot);
    }
  },
  //Filter with computed
  //Au niveau de la carte on remplace le datas par filteredCards qui va agir comme le nouvel array filtré
  //.match pour vérifier par rapport à un String
  //.includes pour vérifier par rapport à un Array de Strings
  // element.level.includes(
  //         this.persSkillGot 
  //       ) || element.role.includes(
  //         this.persSkillGot 
  //Fonctionne sur le level et le role .push level et role dans un tableau séparé ?
  computed: {
    filteredCards(){
      return this.datas.filter((element)=>{
        return  this.persSkillGot.every((item)=>{
          return (
          item.includes(element.level) || 
          item.includes(element.role) ||
          item.includes(element.languages[0])||
          item.includes(element.languages[1])||
          item.includes(element.languages[2])||
          item.includes(element.tools[0])||
          item.includes(element.tools[1])
          )
        })
      })
    }
  }
};

</script>

<style lang="scss">
html {
  background-color: hsl(180, 52%, 96%);
  height: 100vh;
  position: relative;
}
.top {
  background-color: hsl(180, 8%, 52%);
}
.filter {
  position: absolute;
  top: 120px;
  background-color: white;
}
.glob-btn{
  height: 30px;

}
</style>
