<template>
  <div id="calendar-root">
    <div id="calendar-header">
      <div id="month-prev-cont">
        <svg @click="prevMonth()" height="20px" id="Layer_1" style="enable-background:new 0 0 128 128;" version="1.1" viewBox="0 0 128 128" width="20px" xml:space="preserve" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><g><line style="fill:none;stroke:#2F3435;stroke-width:12;stroke-linecap:square;stroke-miterlimit:10;" x1="87.5" x2="40.5" y1="111" y2="64"/><line style="fill:none;stroke:#2F3435;stroke-width:12;stroke-linecap:square;stroke-miterlimit:10;" x1="40.5" x2="87.5" y1="64" y2="17"/></g></svg>
      </div>
      <div id="month-text-cont">{{currentMonth}}</div>
      <div id="month-next-cont">
        <svg @click="nextMonth()" height="20px" id="Layer_1" style="enable-background:new 0 0 128 128;" version="1.1" viewBox="0 0 128 128" width="20px" xml:space="preserve" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><g><line style="fill:none;stroke:#2F3435;stroke-width:12;stroke-linecap:square;stroke-miterlimit:10;" x1="40.5" x2="87.5" y1="17" y2="64"/><line style="fill:none;stroke:#2F3435;stroke-width:12;stroke-linecap:square;stroke-miterlimit:10;" x1="87.5" x2="40.5" y1="64" y2="111"/></g></svg>
      </div>
      </div>
    <div id="calendar-body">
      <Weekdays></Weekdays>
      <Month year="2018" month="this.selectedMonth"></Month>
    </div>
    <div id="calendar-footer"></div>

  </div>
</template>

<script>
import Weekdays from './Weekdays.vue';
import Month from './Month.vue';

export default {
  name: 'Calendar',
  components:{Weekdays, Month},
  data () {
    return {
      months:["January", "February","March","April", "May", "June", "July", "Auguest","September", "Octomber","November", "December"],
      currentMonth: "",
      msg: 'Welcome to Your Vue.js App',
      selectedMonth:0,
      selectedYear:0
    }
  },
  methods:{
     init:function(){
        this.currentMonth = this.months[(new Date()).getMonth()];
        this.selectedMonth = this.getIndexOfMonth(this.currentMonth);
     },
     nextMonth:function(){
        let currentMonthIndex = this.getIndexOfMonth(this.currentMonth);
        let nextIndex = currentMonthIndex+1;
        this.selectedMonth = nextIndex;
        if(this.months.length > nextIndex  || this.months.length-1 == nextIndex){
          this.currentMonth = this.months[currentMonthIndex+1];
        }
     },
     prevMonth:function(){
        let currentMonthIndex = this.getIndexOfMonth(this.currentMonth);
        let nextIndex = currentMonthIndex-1;
        this.selectedMonth = nextIndex;
        if(0 < nextIndex || 0 == nextIndex){
          this.currentMonth = this.months[currentMonthIndex-1];
        }
     },
     getIndexOfMonth: function(month){
       return this.months.indexOf(month);
     }
  },
  mounted(){
    this.init();
  }
}
</script>

<style scoped>
#calendar-header{
    background-color:  #c1212133;
    height: 25px;
    padding: 10px;
    margin-left: 10%;
    margin-right: 10%;
}

#calendar-header div{
   float:left;
}

#prev{
  float:left;
}

#next{
    float: right;
}

#month-prev-cont{
  width:15%;
  text-align: left;
  cursor: pointer;
}

#month-next-cont{
  width:15%;
  text-align: right;
  cursor: pointer;
}

#month-text-cont{
  margin: 0 auto;
  width:70%;
  text-align: center;
}

#calendar-body{
   padding: 10px;
   background-color: #f1f0f0;
   height: 200px;
   margin-left: 10%;
   margin-right: 10%;
}

#calendar-footer{
   background-color:  #c1212133;
   height: 25px;
   padding:5px;
   margin-left: 10%;
   margin-right: 10%;
}

@media only screen and (max-width: 400px) {
 /* #calendar-header{
    width: 100%;
  }

  #calendar-body{
    width: 100%;
  }

  #calendar-footer{
    width: 100%;
  }*/
}


</style>
