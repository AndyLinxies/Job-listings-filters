<template>
  <div class="mt-16">
    <div
      class="h-32 w-3/5 bg-white grid grid-cols-3 gap-4 items-center justify-center text-gray-700 font-semibold shadow-xl rounded-md ml-64"
    >
      <!--Profile picture -->
      <div class="profilePic ml-10">
        <img width="70px" src="../assets/photosnap.svg" alt="" />
        <!-- <img :src="pic" alt=""> -->
      </div>
      <!-- infos -->
      <div class="profileInfos ">
        <div class="topProfInf">
          <span class="text-xs">{{ inData.company }}</span>
          <span class="bg-green-400 rounded-xl p-1 text-white ml-2 mr-2 text-sm">{{ inData.new ? "NEW!" :null }}</span>
          <span class="bg-black rounded-xl p-1 text-white ml-2 mr-2 text-sm">{{ inData.featured ? "FEATURED" :null }}</span>
        </div>
        <div>
            <p>{{inData.position}}</p>
        </div>
        <div>
            <span>{{inData.postedAt}}</span>
            <span>{{inData.contract}}</span>
            <span>{{inData.location}}</span>
        </div>
      </div>
      <!-- skills & position & tools-->
      <div class="skills">
          <button @click="skill" class="bg-green-400 text-white mr-1 mb-1 rounded-xl p-1">{{inData.role}}</button>
          <button @click="skill" class="bg-green-400 text-white mr-1 mb-1 rounded-xl p-1">{{inData.level}}</button>
          <button @click="skill" class="bg-green-400 text-white mr-1 mb-1 rounded-xl p-1" v-for="(lang,index) in inData.languages" :key="index">
              {{lang}}
          </button>
          <button  @click="skill" class="bg-green-400 text-white mr-1 mb-1 rounded-xl p-1" v-for="(tool) in inData.tools" :key="tool">
              {{tool}}
          </button>
          
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    inData: Object,
  },
  data() {
      return {
          
          elemSkill:""
      }
  },
  methods: {
      //Get the value of pressed button
      skill(e){
          
            //console.log(e.target.innerText);
            this.elemSkill=e.target.innerText
            // this.persSkill.push(e.target.innerText)
            // console.log(this.persSkill);
            //create perevent to pass persSkill to parent
            this.$emit('getSkill',this.elemSkill)
      }
  },
};
</script>

<style></style>
