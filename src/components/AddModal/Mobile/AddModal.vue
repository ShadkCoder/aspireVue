<template>
   <div class="am-overlay">
   <div class="am-parent">
   <input v-model="cardname" placeholder="Card Name" :class="{'cardname': true, 'errorname': this.errorname}"/>
   <button class="addbtn" @click="addCard">Add Card</button>
   <div class="am-close" @click="closeAM">X</div>
   </div>
   </div>
</template>

<script>
import {mapGetters} from 'vuex';
export default {
  name: 'AddModal',
  data() {
    return {
      cardname:'',
      errorname:false
    }
  },
  methods:{
    addCard(){
      if(this.cardname != ''){
        this.$store.commit('toggleAddModal',false)
        let pushCard = {}
        pushCard.Name = this.cardname
        pushCard.cardNo = (Math.random().toFixed(16).split('.')[1]).toString()
        pushCard.cvv = Math.random().toFixed(3).split('.')[1]
        pushCard.uid = this.getList.length
        this.$store.commit('updateUids',pushCard.uid)
        pushCard.expiry = '12/27'
        this.$store.commit('updateList',pushCard)
      } 
      else{
        this.errorname = true
      }  
    },
    closeAM(){
      this.$store.commit('toggleAddModal',false)   
    }
  },
  computed:{
      ...mapGetters({
      getList : 'getList'
      })
  },
}
</script>
<style>
.am-overlay{
    position: fixed;
    width: 100%;
    height: 100vh;
    background-color: rgba(0,0,0,0.5);
    top: 0px;
    left: 0px;
    z-index: 10;
}
.am-parent{
    position:fixed;
    background-color:#fff;
    box-shadow: 5px 10px 8px 10px rgba(0,0,0,.5);
    z-index:11;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
    border-radius:5px;
    padding:40px 30px;
}
.cardname{
    border-width: 0px 0px 1px 0px;
    font-size: 20px;
    outline: none;
}
.cardname:focus{
    border-color: goldenrod;
}
.addbtn{
  width: 120px;
    height: 40px;
    cursor: pointer;
    background-color: #0C365A;
    outline: none;
    color: #fff;
    font-weight: 600;
    border: 0px;
    margin-top: 25px;
    border-radius: 6px;
}
.cardname.errorname{
border-color:red;
}
.am-close{
  position: absolute;
    right: 9px;
    top: 7px;
    font-weight: 600;
    padding: 4px;
}
</style>