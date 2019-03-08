<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      temporary
      app
    >
      <v-list>
        <v-list-tile
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title v-text="item.title" />
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-navigation-drawer
      v-model="rightDrawer"
      :right="right"
      temporary
      fixed>
      <v-list>
        <v-list-tile @click.native="right = !right">
          <v-list-tile-action>
            <v-icon light>compare_arrows</v-icon>
          </v-list-tile-action>
          <v-list-tile-title>Switch drawer (click me)</v-list-tile-title>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>    
    <v-toolbar
      :fixed="false"
      :clipped-left="clipped">
      <v-toolbar-side-icon @click="drawer = !drawer" />
      <v-btn
        icon
        @click.stop="miniVariant = !miniVariant"
      >
        <v-icon>{{ `chevron_${miniVariant ? 'right' : 'left'}` }}</v-icon>
      </v-btn>
      <v-btn
        icon
        @click.stop="clipped = !clipped"
      >
        <v-icon>web</v-icon>
      </v-btn>
      <v-btn
        icon
        @click.stop="fixed = !fixed"
      >
        <v-icon>remove</v-icon>
      </v-btn>
      <v-toolbar-title v-text="title" />
      <v-btn
        icon
        @click.stop="rightDrawer = !rightDrawer">
        <v-icon>menu</v-icon>
      </v-btn>
    </v-toolbar>
    <v-content color="white">

        <Table></Table>


    </v-content>
    <!-- <v-footer
      :fixed="fixed"
      app
    >
      <span>&copy; 2019</span>
    </v-footer> -->
  </v-app>
</template>

<script>
import Table from './components/Table.vue'

export default {
  components: {
    Table
  },  
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'bubble_chart',
          title: 'Inspire',
          to: '/inspire'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'ZIM EDITOR'
    }
  }
}
</script>




<style>
a{
  color: #333!important;
}
#loadingPage{
  position: fixed;
  top: 0;
  width: 100%;
  height: 100vh;
  z-index: 99;
  background: url('http://172.104.185.200:8084/assets/imgs/main_loading.gif') no-repeat center white;
  text-align: center;
}
.middle {
    display: flex;
    justify-content: center;
    flex-direction: column;
}
.step{
  position: relative;
}
.editonhover.v-text-field .v-input__append-inner,
.editonhover.v-text-field > .v-input__control > .v-input__slot:before{
    display: none!important;
}
.editonhover.v-text-field:hover > .v-input__control > .v-input__slot:before{
    display: block!important;
}
.editonhover.v-text-field.v-input--is-focused .v-input__append-inner,
.editonhover.v-text-field:hover .v-input__append-inner{
    display: inline-flex!important;
}

.stepMenu{
  position: absolute;
  right: 0;
  bottom: 10px;
  z-index: 9;
  opacity: .2;
  cursor: pointer;
}
.theme--dark.v-menu__content{
  max-width: 200px!important;
  box-shadow: none!important;
  text-align: right;
}
.v-text-field.v-input--is-disabled > .v-input__control > .v-input__slot:before{
  border: none!important;
}
.v-text-field.v-input--is-disabled input{
  color: black!important;
}
.step:hover .stepMenu{
  opacity: 1;
  transition: opacity .25s ease-in-out;
  -moz-transition: opacity .25s ease-in-out;
  -webkit-transition: opacity .25s ease-in-out;  
}
.coversheet textarea{
  border: 2px solid grey;
}
.bold{
  font-weight: bold;
}
#satu .v-speed-dial {
  position: relative;
}
#satu .v-speed-dial__list{
  position: fixed!important;
  right: 14px!important;
  left: auto!important;
  bottom: 80px!important;
  width: 64px!important;
}
#satu .nomargin{
  margin: 0!important;
}
#satu .v-tabs__container{
  flex: none;
}
#satu .v-btn,
#satu .v-tabs__div{
  text-transform: none!important;
}
#stickyBar{
  position: absolute;
  width: 100%;
  z-index: 1;
  height: 64px;
  background-color: white;
}
.tableView .stickyBar {
  position: fixed!important;
  top: 0;
  /* top: -30px;
  transform: translateY(30px); */
  transition: transform .3s linear;
  padding-top: 10px;  
}
#satu .tableTabs .v-tabs__item{
  background-color: #ddd;
  border-radius: 8px 8px 0 0;
  margin: 2px;
  font-size: 85%;
  text-shadow: 1px 1px 1px #fff;
  border-top: 3px solid #fff; 
}
#satu .tableTabs .v-tabs__item--active{
  border-radius: 5px 5px 0 0;
  text-shadow: none;
  border-top: 3px solid #666; 
  background-color: #999;
  font-size: 100%;
  color: #fff;
}
#satu .header{
  text-transform: uppercase;
  font-size: 85%;
  text-shadow: 1px 1px 1px #fff;
  text-align: center;
  border-bottom: 1px solid #666;
}
/* #satu .header .bgY{
  border-top: 3px solid #d88c00;
} */

textarea{
  padding: 10px;
  width: 100%;
  height: 200px;
}
textarea:focus{
  outline: none !important;
}
.cardView textarea{
  padding: 0 10px;
}
.coversheet textarea{
  height: 150px!important;
}
.drag_indicator{
  position:absolute;left:4px;cursor:move;width:16px;  
}
.tableView .drag_indicator{
  left:4px;  
}
.cardView .drag_indicator{
  left:10px;
}
.cardView .step{
  display: table;
  width: 100%;
  padding: 0 40px;
}
.cardView .step > .layout{
  margin-bottom: 1px!important;
}
.cardView .step .v-btn--small{
  height: 20px!important;
}
.cardView .step .v-menu{
  height: 30px!important;  
}
.cardView textarea{
  height: 25px;
}
.tableView .borderleft{
  border-left: 1px solid #666;
}

.notdetail a{
  padding: 2px;
}
.notdetail a:focus,
.notdetail a.focus { 
  border: 2px solid #319ae0;
  padding: 0px;
  outline: none;
  display: table;
  width: 100%;  
}
.notdetail a:focus textarea,
.notdetail a.focus textarea{
  padding: 8px;
}
.bgGrey{
  background-color: #ddd;
}
.bgW{
  background-color: #fff;
}
.bgY{
  background-color: rgb(255, 240, 205);
}
.bgG{
  background-color: rgb(217, 233, 211);
}
.bgB{
  background-color: rgb(198, 218, 247);
}
.dragging{
  border: 2px solid #222;
}


#satu .cardView>.layout{
}

#div1 {
  width: 350px;
  height: 70px;
  padding: 10px;
  border: 1px solid #aaaaaa;
}

</style>
