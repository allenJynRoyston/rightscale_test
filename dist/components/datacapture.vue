<template><div class="ui grid"><div class="two column row"><div class="column"><!-- EMPTY (unset)--><h3 v-show="!show.capture"><br/>Joe: &nbsp;<span v-if="capture.field1 != null">{{capture.field1.title}}</span><a class="cursor" v-if="capture.field1 == null" v-on:click="show.capture = true">Unset</a></h3><!-- DROP DOWN (set)--><div class="ui menu" v-show="show.capture"><a class="item">Joe:</a><div class="link item" v-if="saving.data"><span class="text">Saving...</span></div><div class="ui pointing dropdown link item" id="dropdown1" v-show="!saving.data"><span class="text">Options</span><i class="dropdown icon"></i><div class="menu"><div class="header">Available Options</div><div class="item" v-for="o in dropdown.options" v-on:click="capture.field1 = o">{{o.title}}  </div></div></div></div><p v-show="show.warning"> Must select an option from the dropdown before saving.</p></div><!-- BUTTON BEHAVIORS--><div class="column"><div style="margin-top: 18px;"><button class="ui white right labeled icon button left-margin-10" v-if="!show.capture" v-on:click="show.capture = true">Edit<i class="edit icon"></i></button><button class="ui red right labeled icon button left-margin-10" v-if="!show.capture &amp;&amp; capture.field1 != null" v-on:click="capture.field1 = null">Clear<i class="cancel icon"></i></button><button class="ui primary right labeled icon button left-margin-10" v-if="show.capture" v-on:click="saveData()" v-show="!saving.data">Save<i class="save icon"></i></button><button class="ui primary loading button" v-show="saving.data">Saving</button><button class="ui orange right labeled icon button left-margin-10" v-if="show.capture" v-on:click="show.capture = false" :disabled="saving.data">Cancel<i class="cancel icon"></i></button></div></div></div><div style="position: fixed; bottom: 10px; right: 10px;" v-show="saving.complete"><a class="ui green label large" v-on:click="saving.complete = false"><i class="check circle icon"> </i>Saved!</a></div></div></template><script>export default {
  data: function() {
    return {
      dropdown:{
        options: [
          {id: 0, title: "Option A"},
          {id: 1, title: "Option B"},
          {id: 2, title: "Option C"},
          {id: 3, title: "Option D"}
        ]
      },
      capture:{
        field1: null
      },
      show:{
        warning: false,
        capture: false
      },
      saving:{
        data: false,
        complete: null
      },
      
    }
  },
  created:function(){
    var t = this;
    $(function(){
        $('#dropdown1').dropdown()
    })
  },
  methods:{
    saveData: function(){
      var t = this;
      // VALIDATION CHECK
      if(t.capture.field1 == null){
        t.show.warning = true;
      }
      else{
        t.show.warning = false;
        // mock ajax request
        t.saving.data = true;
        
        // PREPARE DATA FOR UPLOAD
        var packet = {
          field1: t.capture.field1
        }
        console.log(JSON.stringify(packet))
        // AJAX REQUEST (disabled)
        /*
        t.saving.data = false;
        t.show.capture = false;
        t.saving.complete = false;
        
        $.ajax({
          type: "POST",
          url: "http://database.location.endpoint",
          data: JSON.stringify(packet),
          success: function(){
            t.saving.data = false;
            t.show.capture = false;
            t.saving.complete = true;
            setTimeout(function(){
              t.saving.complete = true;
            }, 2000)
          },
          error: function(){
            alert("file upload failure")
          }
        });
        */
        
        // MOCK AJAX REQUEST
        setTimeout(function(){
          t.saving.data = false;
          t.show.capture = false;
          t.saving.complete = true;
          setTimeout(function(){
            t.saving.complete = null;
          }, 2000)
        }, 2000)
      }

      
    },
  },
  beforeDestroy:function(){
    
  }
}</script><style lang="css">/* PENDING VUE-EXPRESS UPDATE */</style>