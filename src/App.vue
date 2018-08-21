<template>
  <div id="app">
    <div class="container">
      <div class="panel">
        <h2><i class="icon-down-open"></i>Order Book</h2>
        <div class="icon">
          <i class="icon-cog"></i>
          <i class="icon-info-circled-alt"></i>
        </div>
      </div>
      <div class="table">
        <div class="table-head">
          <div class="bids">
            <div class="headItem" v-for="item in headItem">{{ item }}</div>            
          </div>
          <div class="asks">
            <div class="headItemRev" v-for="item in headItem.reverse()">{{ item }}</div>            
          </div>
        </div>
        <div class="table-body">
        <div class="bids">
           <div class="row" v-for="(bid, index) in dataTable.bids" :style="drowBids(totalBids[index])"> 
            <div class="cell">{{ bid.numberOfOrders }}</div>
            <div class="cell">{{ totalBids[index]}}</div>
            <div class="cell">{{ bid.quantity}}</div>
            <div class="cell">{{ bid.price }}</div>           
          </div> 
        </div>
          <div class="asks">
             <div class="row" v-for="(ask, index) in dataTable.asks" :style="drowAsks(totalAsks[index])">
              <div class="cell">{{ ask.numberOfOrders }}</div>
              <div class="cell">{{totalAsks[index]}}</div>
              <div class="cell">{{ ask.quantity }}</div>
              <div class="cell">{{ ask.price }}</div>
          </div>  
          </div>
              
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import dataTable from '../1.json';
export default {
  name: 'app',
  data () {
    return {
      dataTable,
      headItem: ['Price', 'Amount','Total', 'Count'],
      totBids: [],
      totAsks: []
    }
  }, 
  computed: {
    totalBids(){
      var tempB = 0;
      for(let i = 0; i < this.dataTable.bids.length; i++){
        tempB += this.dataTable.bids[i].quantity;
        this.totBids.push(tempB);
      }
      return this.totBids;
    },
    totalAsks(){
      var tempA = 0;
      for(let i = 0; i < this.dataTable.asks.length; i++){
        tempA += this.dataTable.asks[i].quantity;
        this.totAsks.push(tempA);
      }
      return this.totAsks;
    }   
  },
  methods: {
     drowBids(totBids){
      let lastBids = this.totBids[this.totBids.length - 1];
      let widthBids = totBids * 100 / lastBids;      
     return {       
        background: 'linear-gradient(90deg,transparent '+(100-widthBids)+'%, #dcf4e7 '+widthBids+'%)' 
      }
    },
    drowAsks(totAsks){
      let lastAsks = this.totAsks[this.totAsks.length - 1];
      let widthAsks = totAsks * 100 / lastAsks;      
     return {
        background: 'linear-gradient(270deg, transparent '+(100-widthAsks)+'%, #ffe3ef '+widthAsks+'%)' 
      }
    }
  }
}
</script>