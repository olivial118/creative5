<template>
 <div class="gridtem">
  <div class="feed">
    <div>
      <form v-on:submit.prevent="tweet" class="tweetForm">
<textarea class="textA" v-model="text" placeholder=""/><br/>
<div class="buttonWrap">
  <button class="primary" type="submit">Post</button>
</div>
      </form>
    </div>
   <div class=result>
    <div v-for="item in feed" class="item">
      <p class="idline"><span class="user">{{item.name}}</span><span class="handle">@{{item.username}}</span><span class="time">{{item.created | since}}</span></p>
      <p class="tweet">{{item.tweet}}</p>
    </div>
  </div>
  </div>
 </div>
</template>

<script>
 import moment from 'moment';
 export default {
   name: 'UserFeed',
   data () {
     return {
       text: '',
     }
   },
   created: function() {
     this.$store.dispatch('getFeed');
   },
   filters: {
     since: function(datetime) {
       moment.locale('en', {
 relativeTime: {
   future: 'in %s',
   past: '%s',
   s:  'seconds',
   ss: '%ss',
   m:  '1m',
   mm: '%dm',
   h:  'h',
   hh: '%dh',
   d:  'd',
   dd: '%dd',
   M:  ' month',
   MM: '%dM',
   y:  'a year',
   yy: '%dY'
 }
       });
       return moment(datetime).fromNow();
     },
   },
   computed: {
     feed: function() {
       return this.$store.getters.feed;
     },
   },
   methods: {
     tweet: function() {
       this.$store.dispatch('addTweet',{
         tweet: this.text,
       }).then(tweet => {
 this.text = "";
       });
     },
   }
 }
</script>

<style scoped>
.gridtem {
  display: flex;
  grid-template-areas: 'left right';
}

 .feed {
     width: 50%;
     padding: 30px 30px 30px 30px;
 }
 .tweetForm {
     padding: 10px;
     margin-bottom: 10px;
     background-color: transparent;
     grid-area: left;
 }
 .result {
     grid-area: right;
     width: 50%;
     padding: 30px 30px 30px 30px;
}
 .buttonWrap {
     width: 100%;
     display: flex;
 }
 button {
     margin-left: auto;
     height: 2em;
     font-size: 0.9em;
 }
 textarea {
     width: 100%;
     height: 500px;
     padding: 2px;
     margin-bottom: 5px;
     resize: none;
     box-sizing: border-box;
     border: 2px solid white;
 }
 .item {
     border-bottom: 1px solid #ddd;
     padding: 10px;
 }
 .tweet {
     margin-top: 0px;
     color: white;
 }
 .idline {
     margin-bottom: 0px;
 }
 .user {
     font-weight: bold;
     margin-right: 10px;
 }
 .handle {
     margin-right: 10px;
     color: #666;
 }
 .time {
     float: right;
     color: #666;
 }
 .primary {
    background-color: black;
}
 .textA {
    background-color: transparent;
    color: white;
    font-size: 20px;
}
</style>
