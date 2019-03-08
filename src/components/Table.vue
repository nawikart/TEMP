<template color="white">
  <v-flex color="white" id="satu" pt-3 :class="listView +'View'">
    <div id="loadingPage" class="middle" v-if="loadingPage"></div>

    <v-layout white pt-2 pb-4 px-4>
      <v-flex style="max-width:720px;">
        <h2>
          <!-- <v-icon v-on:click="mainDetails=!mainDetails" v-show="!mainDetails">arrow_drop_down_circle</v-icon>
          <v-icon v-on:click="mainDetails=!mainDetails" v-show="mainDetails">keyboard_arrow_up</v-icon> -->
           Title here...</h2>

          <template>
            <v-tabs class="my-4" fixed-tabs color="#fff">
              <v-tab v-on:click="mainTab='cover'">
                Coversheet
              </v-tab>
              <v-tab v-on:click="mainTab='table'">
                Table & Details
              </v-tab>              
            </v-tabs>
          </template>

        <v-layout v-show="mainTab=='table' && mainDetails" column mt-1>
          <v-flex xs12>
              <v-text-field
                  append-icon="edit"
                  v-on:keyup.enter="stepNumberPrefixBlur()"
                  class="title editonhover"
                  style="max-width: 160px;"
                  maxlength="4"
                  id="stepNumberPrefix"
                  label="Step number Prefix"
                  value="A"></v-text-field>
          </v-flex>
          <!-- <v-flex xs12>
              <zimTags></zimTags>
          </v-flex>
          <v-flex xs12>
              <shareWith></shareWith>          
          </v-flex>           -->
        </v-layout>
      </v-flex>
      <v-flex text-xs-right>
        buttons here
      </v-flex>      
    </v-layout>

    <v-layout white v-show="mainTab=='cover'" coversheet row wrap>
      <v-flex xs12 px-4 py-4 md6>
        <b>Main Goals</b>
        <textarea>...</textarea>
      </v-flex>
      <v-flex xs12 px-4 py-4 md6>
        <b>Others things</b>
        <textarea>...</textarea>
      </v-flex>
      <v-flex xs12 px-4 py-4 md6>
        <b>Material</b>
        <textarea>...</textarea>
      </v-flex>
      <v-flex xs12 px-4 py-4 md6>
        <b>Location & Date, Time</b>
        <textarea>...</textarea>
      </v-flex>                              
    </v-layout>
  
    <div id="stickyBar">
      <v-layout v-show="mainTab=='table'" row wrap>
        <v-flex tableTabs pl-2 sm12 md6 order-xs2 order-md1>
          <v-tabs fixed-tabs height="30" hide-slider color="#fff">
            <v-tab
              v-for="(t, i) in tabs"
              :key="'i'+i"
              v-on:click="activeTab=i"
              :id="'tab-'+ i" v-on:drop="dropTab($event)" v-on:dragover="allowDrop($event)">
              Item {{ i }}
            </v-tab>
            <v-tab
              v-on:click="activeTab=0"
              :id="'tab-'+ i" v-on:drop="dropTab($event)" v-on:dragover="allowDrop($event)"
            >
              add tab <v-icon small right>add</v-icon>
            </v-tab>          
          </v-tabs>
        </v-flex>
        <v-flex sm12 md6 order-xs1 order-md2 text-xs-right>

          <v-menu offset-y>
            <v-btn small
              slot="activator"
              flat
              class="nomargin"
            >
              {{ (showComments) ? 'Show' : 'Hide' }} comments <v-icon>keyboard_arrow_down</v-icon>
            </v-btn>
            <v-list>
              <v-list-tile v-on:click="showComments=true">
                <v-list-tile-title>Show comments</v-list-tile-title>
              </v-list-tile>
              <v-list-tile v-on:click="showComments=false">
                <v-list-tile-title>Hide comments</v-list-tile-title>
              </v-list-tile>                
            </v-list>
          </v-menu> 


          <v-menu offset-y>
            <v-btn small
              slot="activator"
              flat
              class="nomargin"
            >
              {{ listView }} view <v-icon>keyboard_arrow_down</v-icon>
            </v-btn>
            <v-list>
              <v-list-tile v-on:click="listView='table'">
                <v-list-tile-title>Table View</v-list-tile-title>
              </v-list-tile>
              <v-list-tile v-on:click="listView='card'">
                <v-list-tile-title>Card View</v-list-tile-title>
              </v-list-tile>                
            </v-list>
          </v-menu>  

          <v-menu bottom left
              transition="slide-x-transition"
              bottom
              right
              :close-on-content-click="false"
            >
            <v-btn small
              slot="activator"
              flat
              class="nomargin"
            >
              show/hide column <v-icon>keyboard_arrow_down</v-icon>
            </v-btn>
            <v-card>
              <v-card-title>
                  <h3>Show/hide column</h3>
              </v-card-title>
              <v-divider></v-divider>

              <v-card-text>
                <v-layout>
                  <v-flex mr-4>
                      <v-checkbox small
                        color="blue"
                        label="Goal"
                      ></v-checkbox>
                  </v-flex>
                  <v-flex mr-4>
                      <v-checkbox
                        color="blue"
                        label="Content"
                      ></v-checkbox>
                  </v-flex>
                  <v-flex mr-4>
                      <v-checkbox
                        color="blue"
                        label="Method"
                      ></v-checkbox>
                  </v-flex>
                  <v-flex mr-4>
                      <v-checkbox small
                        color="blue"
                        label="Material"
                      ></v-checkbox>
                  </v-flex>
                  <v-flex mr-4>
                      <v-checkbox
                        label="Comment"
                        color="blue"
                      ></v-checkbox>
                  </v-flex>
                  <v-flex>
                      <v-checkbox
                        color="blue"
                        label="Who"
                      ></v-checkbox>
                  </v-flex>                

                </v-layout> 
              </v-card-text>
            </v-card> 
          </v-menu>                         
        </v-flex>
      </v-layout>
      
      <!-- <v-btn v-on:click="activeTab=i" v-for="(t, i) in tabs" :key="'i'+i"
        :id="'xtab-'+ i" v-on:drop="dropTab($event)" v-on:dragover="allowDrop($event)"
          :dark="activeTab == i" :outline="activeTab != i" color="blue">
            {{t}} </v-btn> -->

        <v-layout>
            <v-flex :xs10="showComments">
              <v-layout v-show="mainTab=='table' && listView=='table'" font-weight-bold header wrap pt-1>
                  <v-flex xs1 pb-1 pt-2 px-2 bgGrey style="white-space: nowrap;">Step no.</v-flex>
                  
                  <v-flex xs1 pb-1 pt-2 px-2 bgGrey borderleft v-show="!showComments && listView=='table'">Duration</v-flex>

                  <v-flex xs2 pb-1 pt-2 px-2 bgGrey borderleft>Goal</v-flex>

                  <v-flex :xs3="showComments" :xs2="!showComments" pb-1 pt-2 px-2 bgGrey borderleft>Content</v-flex>

                  <v-flex :xs2="showComments" :xs1="!showComments" pb-1 pt-2 px-2 bgY borderleft>Method</v-flex>
                  
                  <v-flex xs2 pb-1 pt-2 px-2 bgG borderleft>Material</v-flex>

                  <v-flex xs2 pb-1 pt-2 px-2 bgG borderleft>Remark</v-flex>

                  <v-flex xs1 pb-1 pt-2 px-2 bgB borderleft v-show="!showComments && listView=='table'">Who</v-flex>                  
              </v-layout>
            </v-flex>
            <!-- <v-flex xs2 pb-1 pt-2 px-2 bgGrey borderleft>
              Comments
            </v-flex>           -->
        </v-layout>
    </div>
    <div style="display:table;height:64px;"></div>

    <v-layout v-show="mainTab=='table'">
        <v-flex :xs10="showComments">
            <div row :class="['step', {'mb-5': listView=='card'}]" v-show="r.tab == activeTab" v-for="(r, i) in rows" :key="i" :id="'tab'+ r.tab +'-'+ i" :tab="0" :index="i" v-on:hover="rowSelected($event)" draggable="true" v-on:dragstart="drag($event)" v-on:drop="drop($event)" v-on:dragover="allowDrop($event)">
              <div class="stepMenu" v-if="editModePosition.col != 6 && listView=='table'">
                  <v-menu bottom left dark class="flat" transition="slide-x-transition">
                    <v-btn
                      slot="activator"
                      dark
                      icon
                      color="blue"
                      small>
                      <v-icon small>more_vert</v-icon>
                    </v-btn>

                    <v-btn color="blue" small dark v-on:click="addStep(i)"><v-icon small>add</v-icon> empty step</v-btn>
                    <v-btn color="cyan" small dark><v-icon small>add</v-icon> existing step <v-icon right small>more_horiz</v-icon></v-btn>
                    <v-btn color="orange" small dark><v-icon small>add</v-icon> unit header</v-btn>
                    <v-btn color="indigo" small dark><v-icon small>add</v-icon> break</v-btn>
                    <v-btn color="red" small dark><v-icon small>delete</v-icon> delete</v-btn>

                  </v-menu>        
              </div>

              <v-layout row wrap px-3 grey lighten-3 title v-if="listView=='card'" style="border: 1px solid #999!important;">
                <v-flex xs1 pt-2>
                    <span class="drag_indicator">
                      <v-icon>drag_indicator</v-icon>
                    </span>
                    <span class="middle subheading font-weight-bold">
                      A {{ ('0'+(i+1).toString()).substring(('0'+(i+1).toString()).length - 2, ('0'+(i+1).toString()).length) }}
                    </span>
                </v-flex>
                <v-flex xs10 pt-2>
                    <span class="middle subheading font-weight-bold">this is a title</span>
                </v-flex>
                <v-flex text-xs-center xs1 style="border-left: 1px solid #999!important;">
                    
                  <v-menu
                    transition="slide-x-transition"
                    max-width="414"
                    :full-width="true"
                    bottom
                    right
                    :close-on-content-click="false"
                    >
                    <v-btn small
                      slot="activator"
                      flat>
                      Who
                    </v-btn>

                    <v-card>
                      <v-card-text>
                        <textarea placeholder="type here..."></textarea>
                      </v-card-text>
                    </v-card>
                  </v-menu>            
                    
                </v-flex>                 
              </v-layout>

              <v-layout px-3 grey lighten-3 v-if="listView=='card'">
                <v-flex xs12><b>Starttime</b>: 09:30, <b>Duration</b>: 15min</v-flex>  
              </v-layout>
              <v-layout wrap row notdetail wrap>
                <v-flex v-if="listView=='table'" :xs1="listView=='table'" :xs10="listView=='card'" grey lighten-4 pl-3 py-3 :text-xs-center="listView=='table'" style="position: relative;">
                  <span class="drag_indicator">
                    <v-icon v-if="listView=='table'">drag_indicator</v-icon>
                    <v-icon v-if="listView=='table'" class="mt-2" v-show="showDetail!=i" v-on:click="showDetail=i, showhideDetail(i, ('tab'+ r.tab +'-'+ i))">keyboard_arrow_down</v-icon>
                    <v-icon v-if="listView=='table'" class="mt-2" v-show="showDetail==i" v-on:click="showDetail=-1, showhideDetail(-1, '')">keyboard_arrow_up</v-icon>
                  </span>
                  A {{ ('0'+(i+1).toString()).substring(('0'+(i+1).toString()).length - 2, ('0'+(i+1).toString()).length) }}</v-flex>
                
                <v-flex v-show="!showComments" v-if="listView=='table'" :xs1="listView=='table'" :xs12="listView=='card'" :grey="listView=='card'" lighten-3 py-3 pl-3 borderleft :text-xs-center="listView=='table'">{{ r.name }}</v-flex>

                <v-flex v-if="listView=='card'" xs12 px-2 mt-1 py-1 :grey="listView=='card'" lighten-3 font-weight-bold>Goal</v-flex>
                <v-flex :xs2="listView=='table'" :xs12="listView=='card'" :grey="listView=='card'" lighten-3 bgW borderleft>
                  <a :href="'#col1_index_'+ i"
                    v-on:keyup.enter="editMode(1, i)"
                    v-on:keyup.tab="getFocus(1, i)"
                    v-on:click="getFocus(1, i)"
                    v-on:keyup.left="leftArrow(1, i)"
                    v-on:keyup.right="rightArrow(1, i)"
                    v-on:keyup.up="upArrow(1, i)"
                    v-on:keyup.down="downArrow(1, i)"            
                    :id="'col1_index_'+ i">

                    <textarea v-on:keyup="textAreaAdjust('input_col1_index_'+ i)"
                      class="caption"
                      :id="'input_col1_index_'+ i"  
                      solo flat
                      name="input-7-4"
                      >{{ r.goal }}</textarea>
                  </a>
                </v-flex>

                <v-flex v-if="listView=='card'" xs12 px-2 mt-1 py-1 :grey="listView=='card'" lighten-3 bgW font-weight-bold>Content</v-flex>
                <v-flex :xs3="showComments && listView=='table'" :xs2="!showComments && listView=='table'" :xs12="listView=='card'" :grey="listView=='card'" lighten-3 bgW borderleft>

                  <a
                    :href="'#col2_index_'+ i"
                    v-on:keyup.enter="editMode(2, i)"
                    v-on:keyup.tab="getFocus(2, i)"         
                    v-on:click="getFocus(2, i)"
                    v-on:keyup.left="leftArrow(2, i)"
                    v-on:keyup.right="rightArrow(2, i)"
                    v-on:keyup.up="upArrow(2, i)"
                    v-on:keyup.down="downArrow(2, i)"            
                    :id="'col2_index_'+ i">
                    <textarea v-on:keyup="textAreaAdjust('input_col2_index_'+ i)" style="overflow:hidden"
                      class="caption"
                      :id="'input_col2_index_'+ i"  
                      solo
                      flat
                      name="input-7-4">{{ r.content }}</textarea>
                    </a>        

                </v-flex>

                <v-flex v-if="listView=='card'" mt-1 py-1 xs12 px-2 :grey="listView=='card'" lighten-3 bgGrey font-weight-bold>Method</v-flex>
                <v-flex :xs2="showComments && listView=='table'" :xs1="!showComments && listView=='table'" :xs12="listView=='card'" :grey="listView=='card'" lighten-3 bgY lighten-4 borderleft>
                  
                  <a
                    href="#"
                    v-on:keyup.enter="editMode(3, i)"
                    v-on:keyup.tab="getFocus(3, i)"            
                    v-on:click="getFocus(3, i)"
                    v-on:keyup.left="leftArrow(3, i)"
                    v-on:keyup.right="rightArrow(3, i)"
                    v-on:keyup.up="upArrow(3, i)"
                    v-on:keyup.down="downArrow(3, i)"            
                    :id="'col3_index_'+ i"            
                    >
                    <textarea v-on:keyup="textAreaAdjust('input_col3_index_'+ i)" style="overflow:hidden"
                      class="caption"
                      :id="'input_col3_index_'+ i"  
                      solo
                      flat
                      name="input-7-4"            
                      >{{ r.method }}</textarea>
                  </a>
                </v-flex>
                
                <v-flex v-if="listView=='card'" mt-1 xs12 px-2 py-1 bgGrey :grey="listView=='card'" lighten-3 font-weight-bold>Material</v-flex>
                <v-flex :xs2="listView=='table'" :xs12="listView=='card'" :bgG="listView=='table'" :grey="listView=='card'" lighten-3 borderleft>
                  
                  <a
                    href="#"
                    v-on:keyup.enter="editMode(4, i)"
                    v-on:keyup.tab="getFocus(4, i)"            
                    v-on:click="getFocus(4, i)"
                    v-on:keyup.left="leftArrow(4, i)"
                    v-on:keyup.right="rightArrow(4, i)"
                    v-on:keyup.up="upArrow(4, i)"
                    v-on:keyup.down="downArrow(4, i)"            
                    :id="'col4_index_'+ i"               
                    >
                    <textarea v-on:keyup="textAreaAdjust('input_col4_index_'+ i)" style="overflow:hidden"
                      class="caption"
                      :id="'input_col4_index_'+ i"  
                      solo
                      flat
                      name="input-7-4"
                      >{{ r.material }}</textarea> 
                    </a>
                </v-flex>

                <v-flex v-if="listView=='card'" mt-1 xs12 px-2 py-1 :bgGrey="listView=='table'" :grey="listView=='card'" lighten-3 font-weight-bold>Remark</v-flex>
                <v-flex :xs2="listView=='table'" :xs12="listView=='card'" :bgG="listView=='table'" :grey="listView=='card'" lighten-3 borderleft>
                  <a
                    href="#"
                    v-on:keyup.enter="editMode(5, i)"
                    v-on:keyup.tab="getFocus(5, i)"            
                    v-on:click="getFocus(5, i)"
                    v-on:keyup.left="leftArrow(5, i)"
                    v-on:keyup.right="rightArrow(5, i)"
                    v-on:keyup.up="upArrow(5, i)"
                    v-on:keyup.down="downArrow(5, i)"            
                    :id="'col5_index_'+ i">
                    <textarea v-on:keyup="textAreaAdjust('input_col5_index_'+ i)" style="overflow:hidden"
                      class="caption"
                      :id="'input_col5_index_'+ i"  
                      solo
                      flat
                      name="input-7-4"
                      >{{ r.comment }}</textarea>
                    </a>          
                </v-flex>


                <v-flex v-show="!showComments" v-if="listView=='table'" :xs1="listView=='table'" :xs12="listView=='card'" :bgB="listView=='table'" borderleft>
                  <a
                    href="#"
                    v-on:keyup.enter="editMode(6, i)"
                    v-on:keyup.tab="editMode(6, i)"            
                    v-on:click="getFocus(6, i)"
                    v-on:keyup.left="leftArrow(6, i)"
                    v-on:keyup.right="rightArrow(6, i)"
                    v-on:keyup.up="upArrow(6, i)"
                    v-on:keyup.down="downArrow(6, i)"            
                    :id="'col6_index_'+ i"              
                    >
                    <textarea v-on:keyup="textAreaAdjust('input_col6_index_'+ i)" style="overflow:hidden"
                      class="caption"
                      :id="'input_col6_index_'+ i"  
                      solo
                      flat
                      name="input-7-4"
                      >{{ r.who }}</textarea>
                    </a>          
                </v-flex>

                <v-flex xs12 pr-3 mt-1 px-3 py-1 font-weight-bold :grey="listView=='card'" lighten-3 v-if="listView=='card'" style="position: relative;">
                  
                  <div style="position: absolute; left: -32px; top: -4px;">
                    <v-icon v-if="listView=='card'" class="mt-2" v-show="showDetail!=i" v-on:click="showDetail=i, showhideDetail(i, ('tab'+ r.tab +'-'+ i))">keyboard_arrow_down</v-icon>
                    <v-icon v-if="listView=='card'" class="mt-2" v-show="showDetail==i" v-on:click="showDetail=-1, showhideDetail(-1, '')">keyboard_arrow_up</v-icon>
                  </div>

                  Detail        
                </v-flex>
              </v-layout>

              <v-layout row wrap white style="position:relative;box-shadow:0 4px 0 #999 inset;" mb-5 :pt-3="listView=='table'" v-show="i==detail_i">
                <v-flex xs12 text-xs-right v-if="listView=='table'">
                    <v-icon color="red" v-on:click="showDetail=-1, showhideDetail(-1, '')">close</v-icon>
                </v-flex>
                <v-flex xs12 :px-3="listView=='table'">

                    <textarea v-if="listView=='card'" class="grey lighten-3 pt-3"
                      :id="'card_input_detail_index_'+ i" style="border:1px solid #f00;height:75px!important; overflow:hidden"
                      v-on:keyup="textAreaAdjust('card_input_detail_index_'+ i)"
                      box
                      height="620">{{ r.detail }}</textarea>

                    <textarea v-if="listView=='table'" class="grey lighten-3 pt-3"
                      :id="'tbl_input_detail_index_'+ i" style="border:1px solid #f00;height:75px!important;overflow:hidden"
                      v-on:keyup="textAreaAdjust('tbl_input_detail_index_'+ i)"
                      box
                      height="620"
                      label="Detail">{{ r.detail }}</textarea>            
              
                </v-flex>
              </v-layout>
            </div>
        </v-flex>
        <v-flex xs2 pl-2 white v-show="showComments">
          
                <template>
                  <v-card v-for="i in 3" :key="'c'+ i"
                    class="mx-auto mb-2"
                    color="#26c6da"
                    dark
                    max-width="400"
                  >
                    <v-card-title>
                      <v-icon
                        large
                        left
                        small
                      >
                        comment
                      </v-icon>
                      <span class="subheading font-weight-light">Title here</span>
                    </v-card-title>

                    <v-card-text class="body-1 font-weight-bold">
                      "Turns out semicolon-less style is easier and safer in TS because most gotcha edge cases are type invalid as well."
                    </v-card-text>

                    <v-card-actions>
                      <v-list-tile class="grow">
                        <v-list-tile-avatar color="grey darken-3">
                          <v-img
                            class="elevation-6"
                            src="https://avataaars.io/?avatarStyle=Transparent&topType=ShortHairShortCurly&accessoriesType=Prescription02&hairColor=Black&facialHairType=Blank&clotheType=Hoodie&clotheColor=White&eyeType=Default&eyebrowType=DefaultNatural&mouthType=Default&skinColor=Light"
                          ></v-img>
                        </v-list-tile-avatar>

                        <v-list-tile-content>
                          <v-list-tile-title class="caption">Evan You</v-list-tile-title>
                        </v-list-tile-content>

                        <v-layout
                          align-center
                          justify-end
                          class="caption"
                        >
                          <v-icon class="mr-1" small>favorite</v-icon>
                          <span class="mr-2">256</span>
                          <span class="mr-1">·</span>
                          <v-icon class="mr-1" small>share</v-icon>
                          <span>45</span>
                        </v-layout>
                      </v-list-tile>
                    </v-card-actions>
                  </v-card>
                </template>          
          
        </v-flex>        
    </v-layout>

    <v-dialog v-model="dialogShare" persistent max-width="490">
      <v-card>
        <v-card-title class="headline">Shared With</v-card-title>
        <v-card-text>
          <shareWith></shareWith>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="green darken-1" flat @click="dialogShare = false">appy</v-btn>
          <v-btn color="green darken-1" flat @click="dialogShare = false">cancel</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-dialog v-model="dialogTags" persistent max-width="490">
      <v-card>
        <v-card-title class="headline">Add Tags</v-card-title>
        <v-card-text>
          <zimTags></zimTags>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="green darken-1" flat @click="dialogTags = false">appy</v-btn>
          <v-btn color="green darken-1" flat @click="dialogTags = false">cancel</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <p>&nbsp;</p><p>&nbsp;</p>

    <v-speed-dial v-show="mainTab=='table'"
          :open-on-hover="false"
          right
          bottom
          direction="top"
          transition="slide-y-reverse-transition">
          <v-btn v-on:click="zimActions=!zimActions"
            slot="activator"
            color="blue darken-2"
            dark
            fixed
            bottom
            right
            fab
          >
            <v-icon>more_vert</v-icon>
          </v-btn>

          <!-- <v-btn v-if="!zimActions" v-on:click="zimActions=!zimActions"
            slot="activator"
            color="blue darken-2"
            dark
            fixed
            bottom
            right
            fab
          >
            <v-icon color="red">close</v-icon>
          </v-btn> -->


          <v-btn
            fab
            dark
            small
            color="cyan"
          >
            <v-icon>file_copy</v-icon>
          </v-btn>
          <v-btn
            fab
            dark
            small
            color="green"
            v-on:click="dialogShare=true"
          >
            <v-icon>share</v-icon>
          </v-btn>
          <v-btn
            fab
            dark
            small
            color="pink"
            v-on:click="dialogTags=true"
          >
            <v-icon right>labels</v-icon>
          </v-btn>
          
          <v-btn
            fab
            dark
            small
            color="red"
          >
            <v-icon>delete</v-icon>
          </v-btn>
      </v-speed-dial>
  </v-flex>
</template>


<script>
import zimTags from './zimEditor/zimTags.vue'
import shareWith from './zimEditor/shareWith.vue'

export default {
  components: {
    zimTags, shareWith
  },
  layout: 'default',
  data () {
    return {
      showComments: false,
      loadingPage: true,
      i:0,
      mainTab: 'cover',
      detail_i: -1,
      showDetail: -1,
      mainDetails: true,
      dialogShare: false,
      dialogTags: false,
      listView: 'card',

      zimActions: true,
      activeTab: 0,
      tabs: ['satuuu', 'duaaa', 'tigaaa'],
      rows: [
              {'name': 'satu', 'tab': 0,
                'goal': '111111111The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'content': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'method': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'material': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'comment': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'who': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'detail': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.'
              },

              {'name': 'dua', 'tab': 0,
                'goal': '2222222222The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'content': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'method': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'material': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'comment': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'who': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'detail': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.'
              },

              {'name': 'tiga', 'tab': 0,
                'goal': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'content': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'method': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'material': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'comment': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'who': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'detail': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.'
              },

              {'name': 'empat', 'tab': 1,
                'goal': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'content': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'method': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'material': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'comment': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'who': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'detail': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.'
              },

              {'name': 'lima', 'tab': 1,
                'goal': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'content': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'method': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'material': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'comment': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'who': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'detail': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.'
              },

              {'name': 'sepuluh', 'tab': 1,
                'goal': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'content': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'method': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'material': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'comment': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'who': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'detail': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.'
              },

              {'name': 'sembilan', 'tab': 1,
                'goal': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'content': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'method': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'material': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'comment': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'who': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'detail': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.'
              },

              {'name': 'enam', 'tab': 2,
                'goal': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'content': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'method': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'material': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'comment': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'who': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'detail': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.'
              },

              {'name': 'tujuh', 'tab': 2,
                'goal': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'content': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'method': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'material': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'comment': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'who': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'detail': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.'
              },

              {'name': 'delapan', 'tab': 2,
                'goal': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'content': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'method': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'material': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'comment': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'who': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
                'detail': 'The Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.'
              }
            ],
      stepMenuItems: [
        { title: 'add block/group' },
        { title: 'add break' }
      ],

      isEditMode: false,
      editModePosition: {col: 0, i: 0}
    }
  },

  methods: {
    stepNumberPrefixEditModeChange(){

    },
    stepNumberPrefixBlur(){
      document.getElementById('stepNumberPrefix').blur();
    },
    textAreaAdjust(id) {
      var e = document.getElementById(id)
      // alert(e.scrollHeight)
      e.style.height = "1px";
      e.style.height = (25 + e.scrollHeight) + "px";
    },
    
    addStep(i){
      var rows = []
      for(let r=0; r<this.rows.length; r++){
        rows.push(this.rows[r]) 
        if(r==i){
          rows.push({'name': '&nbsp;', 'tab': 0})
        }
      }
      this.rows = rows
      this.$forceUpdate()
      console.log(this.rows)
    },

    showhideDetail(i, anchor){
      this.detail_i = i
      if(anchor != ''){
        window.location.href = "#detail"+ i;
      }      
    },

    editMode(col, i){
      this.isEditMode = true
      this.editModePosition = {col: col, i: i}
      document.getElementById('input_col'+ col +'_index_'+ i).focus();
    },

    getFocus(col, i){
      this.isEditMode = false
      this.editModePosition = {col: 0, i: 0}
      document.getElementById('col'+ col +'_index_'+ i).focus();
      // document.getElementById('col'+ col +'_index_'+ i).classList.add("focus");   
    },

    leftArrow(col, i){
      if(!this.isEditMode){
        document.getElementById('col'+ (col-1).toString() +'_index_'+ i.toString()).focus()
      }
    },

    rightArrow(col, i){
      if(!this.isEditMode){
        document.getElementById('col'+ (col+1).toString() +'_index_'+ i.toString()).focus()
      }
    },

    upArrow(col, i){
      if(!this.isEditMode){
        document.getElementById('col'+ col.toString() +'_index_'+ (i-1).toString()).focus()
      }
    },
    
    downArrow(col, i){
      if(!this.isEditMode){
        document.getElementById('col'+ col.toString() +'_index_'+ (i+1).toString()).focus()
      }
    },

    allowDrop(ev) {
      ev.preventDefault();
    },

    drag(ev) {
      ev.dataTransfer.setData('text/plain', null);

      let id = ev.target.id
      this.dragElId = id
      document.getElementById(id).classList.add("dragging");
    },

    drop(ev) {
      let id = ev.currentTarget.getAttribute('id')
      ev.preventDefault();
      this.listUpdate(this.dragElId, id)
      document.getElementById(this.dragElId).classList.remove("dragging");
    },

    dropTab(ev) {
      alert(this.dragElId)
      let tid = (ev.currentTarget.getAttribute('id')).split('-')
      let dragEl = this.dragElId.split('-')
      this.rows[parseInt(dragEl[1])].tab = tid[1]
      
      let data = []
      let init = true
      for(let i = 0; i<this.rows.length; i++){
        if(this.rows[i].tab == tid[1] && init == true){ 
          init = false
          data.push(this.rows[parseInt(dragEl[1])])
        }
        if(parseInt(dragEl[1]) != i){
          console.log("added")
          data.push(this.rows[i])
        }
        console.log(dragEl[1] + '----' + i.toString())
        console.log(data[i])  
      }

      this.rows = data

      ev.preventDefault();
      this.$forceUpdate()
    },

    listUpdate(dragElId, dropElId) {  
      let dragEl = dragElId.split('-')
      let dropEl = dropElId.split('-')

      let data = this.rows
      let temp = this.rows[parseInt(dragEl[1])]
      this.rows[parseInt(dragEl[1])] = this.rows[parseInt(dropEl[1])]
      this.rows[parseInt(dropEl[1])] = temp

      this.rows = data

      this.$forceUpdate()
    }
  },

  mounted(){
    // this.textAreaAdjust('input_col1_index_0')
    this.$nextTick(function () {
      this.loadingPage = false
    })
  },

  beforeMount(){
      if (window.innerWidth <= 600) {
        this.listView = 'card'
      }else{
        this.listView = 'table'
      }

      window.onscroll = function() {
        var stickyBar = document.getElementById("stickyBar");
        if(stickyBar){
            var sticky = 295; //stickyBar.offsetTop;
            if (window.pageYOffset > sticky) {
            // if (window.pageYOffset > (sticky + 30)) {
              stickyBar.classList.add("stickyBar");
            } else {
              stickyBar.classList.remove("stickyBar");
            }
        }
      };
  }
}
</script>