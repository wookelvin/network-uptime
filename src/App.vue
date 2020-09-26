<template>
  <div id="app">
    <div class="d-flex align-items-center justify-content-center statusbox text-white" :class="online?'bg-success':'bg-danger'" v-if="checked">
      <div v-if="online">
        Online
      </div>  
      <div v-else>
        Offline
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import isOnline  from 'is-online';

@Component
export default class App extends Vue {
  online = false;
  checked = false;

  async checkOnline() {
    this.online = await isOnline();
    this.checked = true;
  }

  mounted(){ 
    this.checkOnline();
    setInterval(()=>{ 
      this.checkOnline();
    },5000);
  }


}
</script>


<style lang="scss">
@import 'src/scss/style.scss';
#app, body, html{
  height:100%;
}

.statusbox{ 
  height:100%;
  font-size:3em;
  font-weight: bold;
}


</style>
