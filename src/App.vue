<template>
  <div class="wrapper">
    <div v-for="(item, index) in dropdowns" :key="index">
      <Dropdown
        :placeholder="item.placeholder"
        :isOpen="item.isOpen"
        :isDisabled="item.isDisabled"
        :indexOfDropdown="index"
        @sendtypetoapp="pushAtResultMass"
      />
    </div>
    <div class="dropdown__container"></div>
  </div>
</template>

<script>
import Dropdown from "./components/Dropdown.vue";

export default {
  components: { Dropdown },
  name: "App",

  data() {
    return {
      dropdowns: [
        {
          placeholder: "Выберете значение",
          isOpen: false,
          isDisabled: true,
        },
      ],
      massOfCheckedTypes: [],
    };
  },

  methods: {
    pushAtResultMass: function (typeOfElement, indexOfDropdown) {
      console.log(typeOfElement);
      console.log(indexOfDropdown);
    },

    createMass: function (length) {
      for (length; length == 0; length--) {
        this.massOfCheckedTypes.push(null);
      }
    },

    checkIndex: function (index) {
      console.log(index);
    },
  },
};
</script>

<style lang="scss">
.wrapper {
  position: relative;
  display: flex;
  justify-content: space-around;
  align-items: flex-start;
  height: 100vh;
  background-color: #e5e5e5;
  padding-top: 20%;
}

body {
  margin: 0;
}
</style>
