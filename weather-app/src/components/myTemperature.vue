<template class="flex">
  <div class="my-temp q-ma-md column justify-end items-center bg-white flex-center">
    <div class="my-temp__name q-pb-sm mdi-size-m q-pt-sm">
      {{ name }} / {{ contry }}
    </div>
    <div class="my-temp__value">
      {{ value }}°C
      <a> / </a>
      {{(value * 9) / 5 + 32}}°F
      <a> / </a>
      {{value + 273.15}}K
    </div>
    <div class="my-temp__icon">
      <img
          :src="'https://openweathermap.org/img/wn/' + weather.icon + '@2x.png'"
          :alt="weather.description" />
    </div>
    <div class="my-temp__description q-pb-sm">
      {{ weather.description }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'MyTemperature',

  props: {
    name: {
      type: String,
      default: "",
    },
    contry:
    {
      type: String,
      default: "",
    },
    value: {
      type: Number,
      default: 0,
    },
    weather: {
      type: Object,
      default: {},
    }
  }
}
</script>

<style scoped lang="sass">
.my-temp
  width: auto
  height: auto
  border-radius: 20px
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2)

  &__name
    font-size: 1.25rem
    font-weight: 700
    color: #747bff
    justify-items: center

  &__value
    font-size: 1rem
    font-weight: 700

  &__icon
    height: 60px
    img
      height: 100%

  &__description
    font-size: 1rem
    font-weight: 700
    color: #000000
    justify-items: center
</style>