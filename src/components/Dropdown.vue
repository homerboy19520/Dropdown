<template>
  <div>
    <div class="dropdown">
      <div
        v-on:click="toggle"
        class="selected-item"
        :class="{ 'm-open': isDropdownOpen }"
      >
        <p class="selected-item__placeholder">
          {{ isValue ? isValue : placeholder }}
        </p>
        <svg
          class="dropdown__svg"
          :class="{ dropdown__svg_reverse: isDropdownOpen }"
          width="8"
          height="6"
          viewBox="0 0 8 6"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M0.706206 2.41374L3.29621 5.00374C3.68621 5.39374 4.31621 5.39374 4.70621 5.00374L7.29621 2.41374C7.92621 1.78374 7.47621 0.703735 6.58621 0.703735H1.40621C0.516206 0.703735 0.0762062 1.78374 0.706206 2.41374Z"
            fill="#212122"
          />
        </svg>
      </div>
      <ul class="dropdown__list" v-show="isDropdownOpen">
        <li
          class="dropdown__item"
          v-for="(item, index) in items"
          :key="index"
          :disabled="item.isDisabled"
        >
          <DropdownItem
            :text="item.text"
            :type="item.type"
            :isChecked="item.isChecked"
            :isDisabled="item.isDisabled"
            @getvalue="pushAtMass"
            @sendtypetodropdown="sendTypeToApp"
          />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import DropdownItem from "./DropdownItem.vue";

export default {
  name: "Dropdown",
  components: { DropdownItem },
  data() {
    return {
      items: [
        {
          text: "Normal",
          type: "normal",
          isDisabled: false,
        },
        {
          text: "Длинное название пункта, которое занимает сразу несколько строк Длинное название пункта, которое занимает сразу несколько строк Длинное название пункта, которое занимает сразу несколько строк",
          type: "normal",
          isDisabled: false,
        },
        {
          text: "Disabled",
          type: "normal",
          isDisabled: true,
        },
        {
          text: "Selected",
          type: "selected",
          isDisabled: false,
        },
        {
          text: "Длинное название пункта, которое занимает сразу несколько строк ",
          type: "selected",
          isDisabled: false,
        },
        {
          text: "Disabled Selected",
          type: "selected",
          isDisabled: true,
          isChecked: true,
        },
        {
          text: "Normal Danger",
          type: "error",
          isDisabled: false,
        },
        {
          text: "Длинное название пункта, которое занимает сразу несколько строк",
          type: "error",
          isDisabled: false,
        },
        {
          text: "Disabled Error",
          type: "error",
          isDisabled: true,
        },
      ],

      isValue: "",
      isDropdownOpen: this.isOpen,
    };
  },

  props: {
    placeholder: {
      type: String,
      require: true,
    },
    isOpen: {
      type: Boolean,
      require: false,
    },
    isDisabled: {
      type: Boolean,
      require: true,
    },
    indexOfDropdown: {
      type: Number,
    },
  },

  methods: {
    toggle: function () {
      this.isDropdownOpen = !this.isDropdownOpen;
    },

    choseItem: function (text) {
      this.toggle();
      this.title = text;
    },

    pushAtMass: function (value) {
      this.isValue = value;
      this.isDropdownOpen = false;
    },

    sendTypeToApp: function (typeOfComponent) {
      this.$emit("sendtypetoapp", typeOfComponent, this.indexOfDropdown);
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap");
.dropdown {
  min-width: 340px;
  max-width: 340px;
  box-sizing: border-box;
  border-radius: 32px;
  background-color: #fff;
  overflow: hidden;
  box-shadow: 0px 19px 38px rgba(33, 38, 44, 0.15),
    0px 15px 12px rgba(33, 38, 44, 0.11);
  transition: border-radius 0.2s ease-out, background-color 0.2s ease-out,
    color 0.2s ease-out;
  cursor: pointer;
  z-index: 1;

  & .selected-item {
    position: relative;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 9px 20px 9px 20px;
    z-index: 1;

    &::after {
      content: "";
      display: none;
      position: absolute;
      width: calc(100% - 20px);
      height: 1px;
      background-color: #dadee7;
      bottom: 0;
      right: 0;
    }

    &.m-open {
      &::after {
        display: block;
      }
    }

    &__placeholder {
      font-family: "Roboto", sans-serif;
      font-style: normal;
      font-weight: 400;
      font-size: 15px;
      line-height: 18px;
      color: #212122;
      margin: 0;
      transition: background-color 0.2s ease-out;
      user-select: none;
      -ms-text-overflow: ellipsis;
      -o-text-overflow: ellipsis;
      text-overflow: ellipsis;
      overflow: hidden;
      -ms-line-clamp: 1;
      -webkit-line-clamp: 1;
      line-clamp: 1;
      display: -webkit-box;
      display: box;
      word-wrap: break-word;
      -webkit-box-orient: vertical;
      box-orient: vertical;
    }
  }

  &__list {
    position: relative;
    padding: 0;
    margin: 0;
    z-index: 1;
  }

  &__item {
    list-style: none;
    cursor: pointer;
    transition: background-color 0.2s ease-out, color 0.2s ease-out;
    display: flex;
    justify-content: space-between;
    flex-direction: column;
    align-items: center;
  }

  & svg path {
    transition: fill 0.2s ease-out;
  }

  & p {
    margin: 0;
    transition: color 0.2s ease-out;
  }

  &__svg {
    transition: transform 0.2s ease-out;
    position: absolute;
    right: 20px;
    &_reverse {
      transform: rotate(180deg);
    }
  }

  &__container {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    z-index: 0;
  }
}
</style>
