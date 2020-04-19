<template>
  <div class="hello">
    <div class="wrapper">
      <div class="left">
        <div class="title">
          <input type="checkbox" v-model="checked" @change="isAllcheck">
          <span>列表</span>
        </div>
        <ul class="list">
          <li v-for="item in leftList" :key=item.id>
            <label>
              <input type="checkbox" :value=item.id v-model="isSelect" @change="ischeck">
              {{item.name}}
            </label>
          </li>
        </ul>
      </div>
      <div class="change">
        <button class="toLeft" @click="toLeft">向左</button>
        <button class="toRight" @click="toRight">向右</button>
      
      </div>
      <div class="right">
        <div class="title">
          <input type="checkbox" v-model="checked2" @change="isAllcheck2">
          <span>列表</span>
        </div>
        <ul class="list">
          <li v-for="item in rightList" :key=item.id>
            <label>
              <input type="checkbox" :value=item.id v-model="isSelect2" @change="ischeck2" >{{item.name}}
            </label>  
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data(){
    return{
      leftList:[{id:1,name:"数据1"},
                {id:2,name:"数据2"},
                {id:3,name:"数据3"},
                {id:4,name:"数据4"},
                {id:5,name:"数据5"},
                {id:6,name:"数据6"},
                {id:7,name:"数据7"}],
      rightList:[],
      isSelect:[],
      isSelect2:[],
      checked:false,
      checked2:false
    }
  },
  methods:{
    isAllcheck(){
      if(this.checked===false){
        this.isSelect=[]
      }else{
        
        this.leftList.forEach(item=>{
          console.log(item)
          this.isSelect.push(item.id)
        })
        
      }
    },
    ischeck(){
      if(this.checked===true){
        this.checked=!this.checked
      }
    },
    isAllcheck2(){
      if(this.checked2===false){
        this.isSelect2=[]
      }else{
        this.rightList.forEach(item=>{
          console.log(item)
          this.isSelect2.push(item.id)
        })
      }
    },
    ischeck2(){
      if(this.checked2===true){
        this.checked2=!this.checked2
      }
    },
    toRight(){
      this.isSelect.forEach(item=>{
      let index = this.leftList.map(item=>item.id).indexOf(item)
      this.rightList.push(this.leftList[index])
      console.log(index)
      this.leftList.splice(index,1)
      })
      this.isSelect=[]
      this.checked=false
      this.rightList.sort((a,b)=>{return a.id-b.id})
    },
    toLeft(){
      this.isSelect2.forEach(item=>{
      let index = this.rightList.map(item=>item.id).indexOf(item)
      this.leftList.push(this.rightList[index])
      console.log(index)
      this.rightList.splice(index,1)
      })
      this.isSelect2=[]
      this.checked2=false
      this.leftList.sort((a,b)=>{return a.id-b.id})

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul,li{
  list-style: none;
  padding:0;
  margin:0;
}
*{
  box-sizing:border-box;
}
.wrapper{
  border:1px solid red;
  display:flex;
  justify-content: center;
  align-items: center;
  padding:20px;
}
.left,.right{
  height:20rem;
  width:8rem;
  border:1px solid lightsteelblue;
  margin:2rem;
}
.title{
  height:10%;
  background-color:lightsteelblue;
}

</style>
