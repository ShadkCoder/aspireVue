<template>
  <div class="base-container">
    <TopDetail />
    <Flicking :options="{ renderOnlyVisible: true}" ref="flicking" @changed="flickChange" @panelChange="resetFlick">
      <CardDetail :details="{idx}" class="flicking-panel" v-for="idx in getList" :key="idx"/>
    </Flicking>
  </div>
  <MoveMenu />
  <AddModal v-if="getModalStatus" />
  <CancelModal v-if="getCancelStatus" />
  <BottomBand />
</template>

<script>
import TopDetail from './TopDetail/Mobile/TopDetail.vue'
import MoveMenu from './MoveMenu/Mobile/MoveMenu.vue'
import Flicking from "@egjs/vue3-flicking";
import CardDetail from './CardDetail/Mobile/CardDetail.vue'
import AddModal from './AddModal/Mobile/AddModal.vue'
import CancelModal from './CancelModal/Mobile/CancelModal.vue'
import BottomBand from './BottomBand/Mobile/BottomBand.vue'
import {mapGetters} from 'vuex';
export default {
  name: 'HomeSection',
  components: {
    TopDetail,
    MoveMenu,
    Flicking,
    CardDetail,
    AddModal,
    CancelModal,
    BottomBand
  },
  mounted(){
    this.$store.commit('updatePanel',this.$refs.flicking.currentPanel) 
  },
  methods: {
    flickChange(){
      this.$store.commit('updatePanel',this.$refs.flicking.currentPanel)
      let checkFreeze = this.getFrozen.includes(this.$refs.flicking.currentPanel.index)
      this.$store.commit('toggleFreeze',!checkFreeze) 
    },
    resetFlick(){
      let panelTarget = this.$refs.flicking.panelCount - 1
      this.$refs.flicking.moveTo(panelTarget)
    }
  },
  computed:{
      ...mapGetters({
      getList:'getList',  
      getFrozen: 'getFrozen',
      getModalStatus: 'getModalStatus',
      getCancelStatus: 'getCancelStatus'
      })
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
@import url("../../node_modules/@egjs/vue3-flicking/dist/flicking.css");

ul {
  list-style-type: none;
  padding: 0;
}
.base-container{
  background-color:#0C365A;
  position: fixed;
  width: 100%;
  z-index: 1;
}
.aspire-flex{display:flex}
</style>
