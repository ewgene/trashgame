<template>
  <div class="hello">
    <div class="top">
      <h1>Выбери правильный бак<br />для сортировки мусора</h1>
      <div class="base-timer">
        <svg class="base-timer__svg" 
          viewBox="0 0 214 214" 
          xmlns="http://www.w3.org/2000/svg">
          <path
            class="base-timer__path-elapsed"
            d="
              M 107, 107
              m -100, 0
              a 100,100 0 1,0 200,0
              a 100,100 0 1,0 -200,0
            "
          ></path>
        </svg>
      </div>
    </div>
    <div class="bins">
      <div class="bin"
        v-for="bin in wasteTypes"
          :id="bin.type"
          :key="bin.type">
          <img :src="require('@/assets/' + bin.background)">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      wasteTypes: [
        {
          type: "recyclable",
          name:"Вторичные",
          color: "#ffab00",
          position: null,
          background: "wastebox_yellow.png"
        },
        {
          type: "mixed",
          name: "Смешанные",
          color: "#6ac000",          
          position: null,
          background: "wastebox_green.png"
        },
        {
          type: "domestic",
          name: "Бытовые",
          color: "#6ac000",
          position: null,
          background: "wastebox_blue.png"
        },
        {
          type: "dangerous",
          name: "Опасные",
          color: "#ff2020",
          position: null,
          background: "wastebox_gray.png"
        }
      ]
    }
  },
  methods: {
    getBinPositions() {
      let bins = document.querySelector('.bins').children
      for(let i = 0; i<this.wasteTypes.length; i++) {
        this.wasteTypes[i].position = bins[i].getBoundingClientRect().x
      }
    }
  },
  mounted() {
    this.getBinPositions()
  }
}
</script>

<style lang="scss">
h3 {
  margin: 40px 0 0;
}
.hello {
  width: 66vw;
  height: 85vh;
  margin: 0 auto;
  background: #fff;
  border-radius: 30px;
  position: relative;
  overflow: hidden;

  .top {
    width: 100%;
  }

  .bins {
    width: 640px;
    margin: 110px auto;
    position: relative;
    text-align: justify;
  }
}
.bin {
  width: 150px;
  height: 208px;
  display: inline-block;
  margin: 0 5px;

  img {
    width: 100%;
  }
}
.base-timer {
  position: relative;
  width: 200px;
  height: 200px;
  margin: 0 auto;

  &__svg {
    transform: scaleX(-1);
    fill: #fff!important;
    stroke: #af63e6;
    stroke-width: 12px;
    stroke-linecap: round;
  }
  
  @keyframes dash {
    from {
      stroke-dashoffset: 628;
    }
    to {
      stroke-dashoffset: 0;
    }
  }
  
  &__path-elapsed {
    stroke-dasharray: 628;
    animation: dash 60s linear forwards;
  }

  &__path-remaining {
    stroke-width: 7px;
    stroke-linecap: round;
    transform: rotate(90deg);
    transform-origin: center;
    transition: 1s linear all;
    fill-rule: nonzero;
    stroke: currentColor;
  }
}
</style>
