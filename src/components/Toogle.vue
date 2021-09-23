<template>
  <div class="toggle-wrapper">
    <label class="toggle">
      <input
        type="checkbox"
        :checked="(mode === 'dark') ? 'checked' : false"
        @change="$emit('toggle')"
      />
      <span class="toggler round"></span>
    </label>
    <span class="mode-icon" v-html="modeIcon" @click="modeItem()"></span>
  </div>
</template>

<script>
import feather from "feather-icons";

export default {
  name: "Toogle",
  props: ['mode'],
  computed: {
    modeIcon () {
      if (this.mode === "dark") {
        return feather.icons.sun.toSvg({ width: 17, color: "rgb(247, 247, 247)" });
      } else {
        return feather.icons.moon.toSvg({ width: 17, color: "rgb(22, 32, 44)" });
      }
    }
  }
}
</script>

<style>
.toggle-wrapper{
  display: flex;
  text-align: center;
  justify-content: right;
}

.mode-icon {
  display: inline-block;
  margin: 18px 0;
}

.toggle {
  position: relative;
  display: inline-block;
  width: 40px;
  height: 20px;
  margin: 20px 5px;
}

.toggle input {
  opacity: 0;
  width: 0;
  height: 0;
}

.toggler {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: var(--dark);
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

.toggler::before {
  position: absolute;
  content: "";
  height: 12px;
  width: 12px;
  left: 4px;
  bottom: 4px;
  background: var(--light-grey);
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

input:checked + .toggler {
  background: var(--medium-grey);
}

input:checked + .toggler::before {
  background: var(--light-dark);
}

input:checked + .toggler::before {
  -webkit-transform: translateX(20px);
  -ms-transform: translateX(20px);
  transform: translateX(20px);
}

.toggler.round {
  border-radius: 34px;
}

.toggler.round::before {
  border-radius: 50%;
}
</style>