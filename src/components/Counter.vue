<template>
  <transition
    :appear="true"
    :enter-active-class="animationStyle()"
    :leave-active-class="animationStyle()"
    mode="out-in"
  >
    <div
      :class="['counter', backgroundColor()]"
      @click.exact="points++"
      @click.shift="points--"
      title="Click to increment &#10;SHIFT + Click to decrement"
    >
      <div class="locationTeam">
        <p>{{ this.$props.locationTeam == "local" ? "Local" : "Guest" }}</p>
      </div>
      <div class="counter-header">
        <h3>{{ name }}</h3>
      </div>
      <div class="counter-body">
        <h1>{{ points }}</h1>
      </div>
    </div>
  </transition>
</template>

<script lang="ts">
import { defineComponent } from "vue";

type styleType = "local" | "guest";

export default defineComponent({
  props: {
    locationTeam: {
      type: String,
      default: "local",
      validator: (value: styleType) => ["local", "guest"].includes(value),
    },
    gols: {
      type: Number,
      default: 0,
    },
    name: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      points: this.$props.gols,
    };
  },
  methods: {
    backgroundColor(): string {
      return this.$props.locationTeam == "local" ? "localTeam" : "guestTeam";
    },
    animationStyle(): string {
      return this.$props.locationTeam == "local"
        ? "animate__animated animate__fadeInLeft"
        : "animate__animated animate__fadeInRight";
    },
  },
});
</script>

<style scoped>
.counter {
  width: 300px;
  border-radius: 15px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px,
    rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px,
    rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
}
.locationTeam {
  display: flex;
  width: 100%;
  justify-content: end;
  align-items: center;
  height: 30px;
  /* margin-right: 15px; */
  /* background-color: red; */
}

.locationTeam p {
  background-color: #277da1;
  height: 95%;
  border-bottom-left-radius: 15px;
  border-start-end-radius: 15px;
  padding: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
  color: #fff;
}

.counter-header {
  color: #fff;
}

.counter-body {
  color: #fff;
}
</style>
