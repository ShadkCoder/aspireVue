<template>
  <div class="move-parent">
    <div class="mp-topmenu aspire-flex">
       <div class="mp-block" @click="freezeClick">
        <div class="mpb-img">
        <img src="../../../assets/Freeze-card.svg" />
        </div>
        <div class="mpb-txt" v-if="getFreezeStatus">
        Freeze Card
        </div>
        <div class="mpb-txt" v-else>
        Unfreeze card
        </div>
       </div>
       <div class="mp-block">
        <div class="mpb-img">
        <img src="../../../assets/Set-spend-limit.svg" />
        </div>
        <div class="mpb-txt">
        Set spend limit
        </div>
       </div>
       <div class="mp-block">
        <div class="mpb-img">
        <img src="../../../assets/GPay.svg" />
        </div>
        <div class="mpb-txt">
        Add to GPay
        </div>
       </div>
       <div class="mp-block">
        <div class="mpb-img">
        <img src="../../../assets/Replace-card.svg" />
        </div>
        <div class="mpb-txt">
        Replace card
        </div>
       </div>
       <div class="mp-block" @click="toggleCancelModal">
        <div class="mpb-img">
        <img src="../../../assets/Deactivate-card.svg" />
        </div>
        <div class="mpb-txt">
        Cancel card
        </div>
       </div>
    </div>
    <div class="mp-widget">
      <div class="mp-tab aspire-flex">
        <div class="aspire-flex">
          <img src="../../../assets/card-detail.svg" />
          <div class="mpt-txt">Card details</div>
        </div>
        <img src="../../../assets/down-arrow.svg" />
      </div>
      <div class="mp-tab aspire-flex mp-last" @click="closeRecentTransact">
        <div class="aspire-flex">
          <img src="../../../assets/recent-transactions.svg" />
          <div class="mpt-txt">Recent transactions</div>
        </div>
        <img src="../../../assets/down-arrow.svg" />
      </div>
      <div class="mp-intel" v-if="toggleRecentTransact">
      <div class="mpi-cell aspire-flex">
        <div class="mpic-image">
        <img src="../../../assets/file-storage.svg" />
        </div>
        <div class="mpic-center">
          <div class="mpic-head">Hamleys</div>
          <div class="mpic-date">20 May 2020</div>
          <div class="mpic-details">
            <div class="mpic-card"><img src="../../../assets/business-and-finance.svg" /></div>
            <div class="mpic-text">Refund on debit card</div>
          </div>
        </div>
        <div class="mpic-amount mpic-credit">+ S$ 150</div>
      </div>
      <div class="mpi-cell aspire-flex">
      <div class="mpic-image">
        <img src="../../../assets/file-storage.svg" />
        </div>
        <div class="mpic-center">
          <div class="mpic-head">Hamleys</div>
          <div class="mpic-date">20 May 2020</div>
          <div class="mpic-details">
            <div class="mpic-card"><img src="../../../assets/business-and-finance.svg" /></div>
            <div class="mpic-text">Charged to debit card</div>
          </div>
        </div>
        <div class="mpic-amount">+ S$ 150</div>
      </div>
      <div class="mpi-cell aspire-flex">
        <div class="mpic-image">
          <img src="../../../assets/file-storage.svg" />
        </div>
        <div class="mpic-center">
          <div class="mpic-head">Hamleys</div>
          <div class="mpic-date">20 May 2020</div>
          <div class="mpic-details">
            <div class="mpic-card"><img src="../../../assets/business-and-finance.svg" /></div>
            <div class="mpic-text">Charged to debit card</div>
          </div>
        </div>
        <div class="mpic-amount">+ S$ 150</div>
      </div>
      </div>
      <div class="mp-alltransact">View all card transactions</div>
    </div>
  </div>
</template>

<script>
import {mapGetters} from 'vuex';

export default {
  name: 'MoveMenu',
  data() {
    return {
      toggleRecentTransact: true,
    }
  },
  methods: {
    freezeClick(){
      if(!this.getFreezeStatus){
        this.$store.commit('removeFrozen',this.getPanel.index)
      }
      else{
        this.$store.commit('updateFrozen',this.getPanel.index)
      }
      this.$store.commit('toggleFreeze',!this.getFreezeStatus)  
    },
    toggleCancelModal(){
      this.$store.commit('toggleCancel',true)   
    },
    closeRecentTransact(){
       this.toggleRecentTransact = !this.toggleRecentTransact
    }
  },
  computed:{
     ...mapGetters({
       getPanel: 'getPanel',
       getFreezeStatus:'getFreezeStatus'
     })
    },
}
</script>
<style>
.move-parent {
    z-index: 2;
    position: relative;
    top: 420px;
    background-color: #EDF3FF;
    border-top-left-radius: 20px;
    border-top-right-radius: 20px;
}
.mpb-txt{
    font-size:13px;
    padding-top: 2px;
    font-weight: 600;
}
.mp-topmenu{
    padding: 20px 0px;
}
.mp-block {
    padding-left: 6px;
}
.mp-widget{
    background-color:#fff;
    min-height:750px;
    padding-top: 24px;
}
.mp-tab {
    font-weight: 600;
    background-color: #FAFCFF;
    padding: 24px 20px;
    border: 1px solid #F5F5F5;
    margin: 0px 24px 24px;
    border-radius: 10px;
    justify-content: space-between;
}
.mp-tab > .aspire-flex{
  align-items:center;
}
.mpt-txt{
  margin-left: 5px;
}
.mp-intel{
  margin: 0px 24px;
  padding: 18px;
  border-left: 1px solid #F0F0F0;
  border-right: 1px solid #F0F0F0;
  position: relative;
  top: -6px;
}
.mp-tab.mp-last{
  margin-bottom:0px;
}
.mpic-image{
  background-color: #009DFF1A;
  border-radius: 100%;
  /* padding: 0px 34px; */
  align-items: center;
  height: 48px;
  width: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.mpic-center{
  position: relative;
  top: 5px;
  font-size: 14px;
  text-align: left;
  margin-left:10px;
}
.mpi-cell.aspire-flex {
    width: 100%;
    border-bottom: 1px solid #F0F0F0;
    padding: 24px 0px;
}
.mpic-head{
  font-weight:600;
  margin-bottom: 4px;
}
.mpic-date{
  color:#AAAAAA;
  font-size:13px;
}
.mpic-card{
  background-color: #325BAF;
  width: 24px;
  height: 24px;
  border-radius: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 8px;
}
.mpic-details{
  display:flex;
  align-items: center;
  margin-top: 14px;
}
.mpic-amount{
  font-weight:600;
}
.mpic-amount.mpic-credit{
color:#01D167
}
.mp-alltransact{
  margin: 0px 24px;
  padding: 18px;
  background-color: #EDFFF5;
  border: 1px solid #DDFFEC;
  position: relative;
  top: -8px;
  border-bottom-left-radius: 8px;
  border-bottom-right-radius: 8px;
  color:#01D167;
  font-weight: 600;
}
</style>