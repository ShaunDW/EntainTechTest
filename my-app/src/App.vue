<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Racing Tracking App"/>
  
    <p>
      <strong>Details of next 5 races</strong>
    </p>
    
   
    <ul>
      Meeting Name: {{ posts.data.race_summaries[races[0].ID].meeting_name }} <br />
      Race Number: {{posts.data.race_summaries[races[0].ID].race_number}}<br />
      Category is: {{ GetCategory(0) }} <br />
      Starting in: {{posts.data.race_summaries[races[0].ID].advertised_start.seconds}} seconds
    </ul>

    <ul>
      Meeting Name: {{ posts.data.race_summaries[races[1].ID].meeting_name }} <br />
      Race Number: {{posts.data.race_summaries[races[1].ID].race_number}}<br />
      Category is: {{ GetCategory(1) }} <br />
      Starting in: {{posts.data.race_summaries[races[1].ID].advertised_start.seconds}} seconds
    </ul>

    <ul>
      Meeting Name: {{ posts.data.race_summaries[races[2].ID].meeting_name }} <br />
      Race Number: {{posts.data.race_summaries[races[2].ID].race_number}}<br />
      Category is: {{ GetCategory(2) }} <br />
      Starting in: {{posts.data.race_summaries[races[2].ID].advertised_start.seconds}} seconds
    </ul>

    <ul>
      Meeting Name: {{ posts.data.race_summaries[races[3].ID].meeting_name }} <br />
      Race Number: {{posts.data.race_summaries[races[3].ID].race_number}}<br />
      Category is: {{ GetCategory(3) }} <br />
      Starting in: {{posts.data.race_summaries[races[3].ID].advertised_start.seconds}} seconds
    </ul>

    <ul>
      Meeting Name: {{ posts.data.race_summaries[races[4].ID].meeting_name }} <br />
      Race Number: {{posts.data.race_summaries[races[4].ID].race_number}}<br />
      Category is: {{ GetCategory(4) }} <br />
      Starting in: {{posts.data.race_summaries[races[4].ID].advertised_start.seconds}} seconds
    </ul>

    
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data() {
    return {
      posts: [],
      races: []
    };
  },

  methods: {

    // Function for calling the API
    async getData() {
      const response = await this.$http.get(
          "https://api.neds.com.au/rest/v1/racing/?method=nextraces&count=10"
        );
      this.posts = response.data;
      this.races.splice(0)

      // Gets the next 5 races to go
      this.races.push({ID:this.posts.data.next_to_go_ids[0]})
      this.races.push({ID:this.posts.data.next_to_go_ids[1]})
      this.races.push({ID:this.posts.data.next_to_go_ids[2]})
      this.races.push({ID:this.posts.data.next_to_go_ids[3]})
      this.races.push({ID:this.posts.data.next_to_go_ids[4]})   
    },

    // Retrives the raceNum, and returns the category type
    GetCategory(raceNum){ 
      if (this.posts.data.race_summaries[this.races[raceNum].ID].category_id == "9daef0d7-bf3c-4f50-921d-8e818c60fe61" ) { return "Greyhound racing" } 
      else if (this.posts.data.race_summaries[this.races[raceNum].ID].category_id == "161d9be2-e909-4326-8c2c-35ed71fb460b" ) { return "Harness racing" }   
      else { return "Horse racing" }
      }

  },


//Calls the API function every 5 seconds
  mounted: function () {
    setInterval(this.getData, 5000)
  }


}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
