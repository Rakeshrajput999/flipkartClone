<template>
     <header>
          <div class="header-left">
            <router-link to="/">
                <a href="#"> Flipkart</a>
            </router-link>
           <div class="header-left-p">
           <p><a href="#">Explore</a> <span>Plus<i class="fas fa-plus"></i></span></p>
        </div>
        </div>
          <div class="header-center">
        <input class="header-center-input" type="text" placeholder=" Search for products,Brands and more"><i class="fas fa-search"></i>
          </div>
          <div class="header-right">
            <div>
              <router-link v-if="!$store.state.token" class="active" to="/login">login</router-link>
              <button v-else class="active" @click="logOut()" >logout</button>
              
            </div>
            <router-link to="/Profile" v-show="$store.state.token">profile<i class="fas fa-sort-down"></i></router-link>
              <div class="locale-changer">
    <select v-model="$i18n.locale">
      <option v-for="locale in $i18n.availableLocales" :key="`locale-${locale}`" :value="locale">{{ locale }}</option>
    </select>
  </div>
            <router-link to="/Cart" v-show="$store.state.token"><i class="fas fa-shopping-cart" ></i></router-link>
          </div>
     </header>
</template>

<script>
import { RouterLink } from 'vue-router'
export default {
  name:'navbar',
  data() {
    return {
      
    }
  },
  updated(){
    this.$store.commit('userAuth')
  },

  methods: {
    async logOut(){
      this.$store.commit('userAuth')
      console.log("logout",this.$store.state.token)
      if(this.$store.state.token){
        localStorage.removeItem('token')
        await this.$store.dispatch('getfackApi')
      }       
    }
  }
}
</script>

<style scoped>
 header{
    display: flex;
    justify-content: space-evenly;
    background-color: #2874f0;
    width: 100%;
    height: 56px;
   position: sticky;
   top: 0px;
   z-index: 1;
 }
 .header-left{
     width: 20%;
     text-align: right;
     margin: 5px 0px;
     cursor: pointer;
 }
 .header-left a{
     color: white;
     font-size: 20px;
     text-decoration: none;
     font-weight: bold;
     font-style: italic;
     letter-spacing: 1.5px;
     
 }
 .header-left-p a{
    font-size: 10px;
    letter-spacing: 1.5px;
 }
 .header-left-p span{
     color: yellow;
     font-size: 10px;
     letter-spacing: 1px;
 }
 .header-left-p:hover{
     text-decoration: underline;
     color: white;
 }
 .header-center{
     width: 40%;
     text-align: left;
     line-height: 50px;
     cursor: pointer;
     padding-left: 10px;
     position: relative;
 }
 .header-center-input{
     height: 36px;
     width: 100%;
     border: none;
     text-align: left;
     padding-left: 20px;
     cursor: pointer;
 }
 .fa-search{
     position: absolute;
     top: 30%;
     left: 94%;
     font-size: 18px;
     color: #2874f0;
 }
 .header-right{
     width: 40%;
     font-size: 15px;
     display: flex;
   justify-content: flex-start;
   text-transform: capitalize;
   line-height: 50px;
 }
 .header-right a ,button{
     text-decoration: none;
     color: white;
     margin: 0px 25px;
 }
 .header-right .active{
     background-color: white;
     color: #2874f0;
     padding: 5px 30px;
     height: 30px;
     width: 130px;
     line-height: 23px;
     margin-top: 8px;
     border-radius: 2px;
     text-align: center;
 }
 .fa-shopping-cart{
     padding-right: 10px;
 }
 .fa-sort-down{
     padding-left: 5px;

 }
</style>




  