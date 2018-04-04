<template>


  <div id="app">

    <div id="theory-A">
      Theory A
      <!-- <img src="./assets/logo.png" class="logo"> -->
    </div>

    <div id="overheard-some-stuff">
      <div v-for="dialogue in dialogues" class="dialogue">
        <span class="yawn">{{dialogue.yawn}}</span>
        <span class="reference" :class="dialogue.styling">
          {{dialogue.reference}}
        </span>
      </div>
    </div>

    <div>

      <addendum/>

    </div>

  </div>


</template>

<script>

  import dialogues from './dialogues.js';
  import addendum from '@/components/addendum.vue';

  export default {
    name: 'app',
    components: {
      addendum
    },
    data: function () {
      return {
        dialogues: dialogues,
        trueApocalypse: false
      }
    },
    mounted: function () {
      // window.onscroll = () => {
      //   const d = document.documentElement;
      //   const offset = d.scrollTop + window.innerHeight;
      //   const height = d.offsetHeight;
      //   const endOfPage = offset === height;
      //   if (endOfPage) {
      //     this.trueApocalypse = true;
      //     window.scroll({
      //       top: 0,
      //       left: 0,
      //       behavior: 'smooth'
      //     });
      //     setTimeout(() => {
      //       this.trueApocalypse = false
      //     }, 3000)
      //   }
      // };
    }

  }

</script>

<style lang="less">

  body { margin: 0px; }
  @soft-fur-grey : #f9f9f9;
  .space-to-breathe() {
    padding: 5px 10px;
    margin: 5px;
    border-top-right-radius: 10px;
    border-bottom-right-radius: 10px;
    background-color: darken(@soft-fur-grey, 3%);
  }

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    padding: 20px;
    background-color: @soft-fur-grey;
    // &.shattered-perception {
    //   text-shadow: 5px 5px #b7b7b7 !important;
    //   filter: invert(1);
    //   transition: all 2s ease;
    // }
  }

  #theory-A {
    font-size: 2rem;
    text-align: center;
    margin-bottom: 5px;
    .logo {
      width: 22px;
    }
  }

  #overheard-some-stuff {
    display: flex;
    flex-direction: column;
    align-items: center;
    .dialogue {
      display: flex;
      align-items: center;
      width: 100%;
      .yawn {
        width: 50%;
        display: inline-block;
        color: darkgrey;
        text-align: right;
        .space-to-breathe();
      }
      .reference {
        width: 50%;
        display: inline-block;
        color: grey;
        text-align: left;
        text-shadow: 0px 0px darken(@soft-fur-grey, 30%);
        &.divine { color: gold; }
        &.sinful { color: maroon; }
        &.rejection { color: steelblue; }
        &.good-intentions { color: black; text-shadow: 2px 0px #a0a0a0; }
        &.false-divinity { color: goldenrod; }
        &.trickster { color: navajowhite; }
        &.firey { color: crimson; }
        &.forgetful { text-shadow: 2px 2px #b7b7b7; }
        &.oblivion{ color: ghostwhite; }
        &.silent{ color: darken(@soft-fur-grey, 5%); }
      }
    }
  }

</style>
