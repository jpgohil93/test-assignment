<template>
  <!-- <div>{{ id }}</div> -->
  <div @click="callCard">
    <div style="position: relative">
      <img
        v-bind:src="data.images[0].url"
        height="200px"
        width="314px"
        style="
          border-radius: 10px;
          border-bottom-left-radius: 0px;
          border-bottom-right-radius: 0px;
        "
      />
      <img
        src="/heart.png"
        height="30"
        width="30"
        v-on:click.stop="callHeart"
        style="position: absolute; right: 8px; top: 8px"
      />
      <div
        v-if="data.isPremium"
        style="
          background-color: rgba(255, 255, 255, 0.5);
          position: absolute;
          left: 5px;
          bottom: 4px;
          border-radius: 20px;
        "
      >
        <label
          style="padding: 4px; font-size: 13px; color: white; font-weight: bold"
        >
          <img src="/trophy.png" height="16" width="16" />Premium Recipe</label
        >
      </div>
    </div>
    <b class="text-recipe">{{ data.title }}</b>
    <div class="row" style="margin-left: 10px">
      <div class="col-sm-3">
        <star-rating
          :rating="data.rating.score"
          :increment="0.5"
          :show-rating="false"
          :star-size="20"
          active-color="#fda01e"
        ></star-rating>
      </div>
      <div class="col-sm-7" style="padding: 5px">
        <label style="color: #1cc98e; font-weight: bold"
          >{{ data.rating.count }} ratings</label
        >
      </div>
    </div>
    <div class="col-sm-12 row" style="margin-left: 10px">
      <div class="col-sm-2 text-size">
        <label
          ><img src="/clock.svg" height="18" width="18" />{{
            data.preparationTimeMinutes | dateFormat
          }}</label
        >
      </div>
      <div class="col-sm-5 text-size">
        <label>
          <img src="/fire.png" height="16" width="16" />
          {{
            data.details.energy
              | checkEnergy(data.details.units.energy, energyType)
          }}
        </label>
      </div>
      <div class="col-sm-5 row">
        <div class="col-sm-4 text-size">
          <label
            ><label style="color: red; font-size: 23px">•</label
            >{{
              data.details.nutrients.carbs + data.details.units.carbs
            }}</label
          >
        </div>
        <div class="col-sm-4 text-size">
          <label
            ><label style="color: blue; font-size: 23px">•</label
            >{{
              data.details.nutrients.proteins + data.details.units.proteins
            }}</label
          >
        </div>
        <div class="col-sm-4 text-size">
          <label
            ><label style="color: #fda01e; font-size: 23px">•</label
            >{{ data.details.nutrients.fats + data.details.units.fats }}</label
          >
        </div>
      </div>
    </div>

    <!-- <p>{{ data.preparationTimeMinutes | dateFormat }}</p>
    <p>
      {{
        data.details.energy | checkEnergy(data.details.units.energy, energyType)
      }}
    </p>
    <p>{{ data.details.nutrients.carbs + data.details.units.carbs }}</p>
    <p>{{ data.details.nutrients.proteins + data.details.units.proteins }}</p>
    <p>{{ data.details.nutrients.fats + data.details.units.fats }}</p> -->
  </div>
</template>

<script>
import StarRating from "vue-star-rating";
// import Vue from "vue";
// Vue.component("star-rating", StarRating.default);
export default {
  props: {
    id: {
      type: String,
      required: true,
    },
    data: {
      type: String,
    },
    energyType: {
      type: String,
    },
  },
  components: {
    StarRating,
  },
  name: "recipe",
  mounted() {
    // this.dateFormat()
  },
  methods: {
    callCard: function () {
      alert("Click on card")
    },
    callHeart: function () {
      alert("Click on heart")
      return
    }
  },
  filters: {
    dateFormat: function (value = 0) {
      // value
      // let ans = parseInt(value/60) === 0 ? ( value%60 + " min") : (parseInt(value/60) + " hr " + value%60 + " min")
      console.log(
        "Val: ",
        parseInt(value / 60) === 0
          ? (value % 60) + " min"
          : parseInt(value / 60) + " hr " + (value % 60) + " min"
      );
      return parseInt(value / 60) === 0
        ? (value % 60) + " min"
        : parseInt(value / 60) + " hr " + (value % 60) + " min";
    },
    checkEnergy: function (value, energy, energyType) {
      let energyNewType = energyType == "calories" ? "kcal" : "kJ";
      let answer = 0;
      if (energy != energyNewType) {
        if (energyNewType == "kcal") {
          answer = value * 4.184;
        } else {
          answer = value / 4.184;
        }
      } else {
        answer = value;
      }
      return parseInt(answer) + " " + energyType;
    },
  },
};
</script>


<style>
.text-recipe {
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  text-overflow: ellipsis;
  display: -webkit-box;
  overflow: hidden;
  padding: 4px;
  min-height: 55px;
}
.text-size label {
  font-size: 15px;
  padding: 0px;
}
.text-size {
  font-size: 15px;
  padding: 0px;
}
</style>