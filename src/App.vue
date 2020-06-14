<template>
  <div id="app">
    <vue-particles
        class="background"
        color="#cadecc"
        :particleOpacity="0.7"
        :particlesNumber="30"
        shapeType="circle"
        :particleSize="4"
        linesColor="#111e6c"
        :linesWidth="1"
        :lineLinked="true"
        :lineOpacity="0.3"
        :linesDistance="250"
        :moveSpeed="3"
        :hoverEffect="true"
        hoverMode="grab"
        :clickEffect="true"
        clickMode="push"
      >
    </vue-particles>
     <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">Why?</router-link>
    </div>
    <router-view/>
    <div class="foreground" v-if="this.$route.path !== '/about'">
      <h3 @mouseover="hover = true"
      @mouseleave="hover = false">{{formattedElapsedTime}}</h3>
    <span v-if="hover && flag">
      Social Distancing since 18th March, 2020
    </span>
    <div class="buttons">
      <button class="button" type="submit" @click="start()">Start</button> |
      <button class="button" type="submit" @click="stop()">Stop</button> |
      <button class="button" type="submit" @click="reset()">Reset</button>
    </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment'
export default {
  name: 'App',
  data () {
    return {
      elapsedTime: moment(),
      startTime: moment('20200318000000', 'YYYYMMDDhhmmss'),
      timer: undefined,
      flag: 1,
      hover: false
    }
  },
  computed: {
    formattedElapsedTime () {
      const seconds = (this.elapsedTime.diff(this.startTime, 'seconds') % 60) + ' seconds '
      const minutes = (this.elapsedTime.diff(this.startTime, 'minutes') % 60) + ' minutes '
      const hours = (this.elapsedTime.diff(this.startTime, 'hours') % 24) + ' hours '
      // const months = this.elapsedTime.diff(this.startTime, 'months') + ' months '
      const days = this.elapsedTime.diff(this.startTime, 'days') + ' days '
      return days + hours + minutes + seconds
    }
  },
  methods: {
    start () {
      this.timer = undefined
      this.timer = setInterval(() => {
        this.elapsedTime = moment()
      }, 1000)
    },
    stop () {
      clearInterval(this.timer)
      this.timer = undefined
    },
    reset () {
      this.timer = undefined
      this.flag = 0
      this.startTime = moment()
      this.elapsedTime = moment()
    }
  },
  beforeMount () {
    this.start()
  }
}
</script>

<style>
#app {
  font-family: Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
  position: relative;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.foreground {
  position: relative;
}

.background{
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
}

button {
  margin-top: 28px;
  width: 80px;
  height: 24px;
  background: #16a085;
  border: none;
  border-radius: 2px;
  color: #fff;
  font-weight: 500;
  transition: 0.1s ease;
  outline: none;
  box-shadow: none;
}

button:hover {
  opacity: 0.8;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  transition: 0.1s ease;
  outline: none;
  box-shadow: none;
}
p span {
  display: block;
}

.buttons {
  position:absolute;
  width:300px;
  height:0px;
  bottom:-140px;
  right:25%;
  left:50%;
  margin-left:-150px;
}
</style>
