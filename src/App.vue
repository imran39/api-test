 <template>
  <h1> api_page</h1>
  <div>

  <ul class="item" v-for="item in list" :key="item.id">
   <li> {{item.id}}</li>
   <li> {{item.email}} </li>
   <li> {{item.first_name}}</li>
   <li>{{item.last_name}}</li>
   <li><img :src="item.avatar"/></li>

   
  </ul>
  <div>
    <jw-pagination :pageSize=8 :items="result" @changePage="onChangePage"></jw-pagination>
  </div>
</div>
</template>

<script>

var result;
import axios from 'axios'
export default {
  name: 'App',
  data(){
    return{
      list:[],
      result
    };
  },
  methods:{
    onChangePage(list){
      console.log(list)
      this.list=list;
    }
  },


  async mounted()
  {
    let result =await axios.get("https://reqres.in/api/users?page=2");
    console.warn("Api data", result.data.data);
    this.list=result.data.data;
  }

};
</script>
<style>
.item{
  display: flex;
}
.item li {
  display: inline-block;
  width: 180px;
  border: 1px solid;
  padding: 5px;
  text-align: center;

}
.item img{
  width: 50px;
}
</style>
