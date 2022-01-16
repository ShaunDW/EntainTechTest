<template>
    <div>
        <h2>Race Tracking App</h2>
        <p v-show="time">
            <strong>Time:</strong> {{ time }}
        </p>
    </div>  
</template>

<script>
    export default {
        name: "DateTime",
        data: () => ({
          time: '',
        }),

        // Function for getting the current time
        methods: {
          showTime: function () {
            this.time = new Date().toLocaleString();             
          },
        },

        // calls the time function every second
        mounted: function () {
          this.time = setInterval(this.showTime, 1000)
        },  
    };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>