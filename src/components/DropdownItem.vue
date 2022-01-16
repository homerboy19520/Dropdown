<template>
  <div
    class="dropdown-item"
    v-on:click="chouseElement"
    :class="[
      {
        'm-selected': type === `selected`,
        'm-checked': isDropdownChecked,
        'm-eror': type === `error`,
        'm-disabled': isDisabled,
      },
    ]"
  >
    <p>{{ text }}</p>
    <svg
      v-show="isDropdownChecked"
      width="14"
      height="12"
      viewBox="0 0 14 12"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
    >
      <path
        d="M4.32915 9.22918L1.43749 6.33751C1.28179 6.18146 1.07042 6.09377 0.849988 6.09377C0.629556 6.09377 0.418181 6.18146 0.262488 6.33751C-0.0625122 6.66251 -0.0625122 7.18751 0.262488 7.51251L3.74582 10.9958C4.07082 11.3208 4.59582 11.3208 4.92082 10.9958L13.7375 2.17917C14.0625 1.85417 14.0625 1.32917 13.7375 1.00418C13.5818 0.848131 13.3704 0.760437 13.15 0.760437C12.9296 0.760437 12.7182 0.848131 12.5625 1.00418L4.32915 9.22918Z"
        fill="#5C6773"
      />
    </svg>
  </div>
</template>

<script>
export default {
  name: "DropdownItem",
  data() {
    return {
      isDropdownChecked: this.isChecked,
    };
  },
  props: {
    text: {
      type: String,
      require: true,
    },
    type: {
      type: String,
      require: true,
    },
    isDisabled: {
      type: Boolean,
      default: false,
    },
    isChecked: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    chouseElement: function () {
      if (this.type === "selected") {
        this.isDropdownChecked = !this.isDropdownChecked;
      } else {
        this.$emit("getvalue", this.text);
      }
      this.$emit("sendtypetodropdown", this.type);
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap");
.dropdown {
  & .dropdown-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    transition: background-color 0.2s ease-out, color 0.2s ease-out;
    padding: 9px 40px 9px 16px;
    box-sizing: border-box;
    position: relative;

    &:hover {
      background-color: #057dff;
      color: #fff;

      & p {
        color: #fff;
      }

      & svg path {
        fill: #fff;
      }
    }

    &:active {
      background-color: #1a53bc;
      color: #fff;
    }

    &.m-disabled {
      background-color: #f1f2f6;
      color: #757575;
      cursor: auto;
      pointer-events: none;

      svg path {
        fill: #757575;
      }
    }

    & svg {
      display: none;
      position: absolute;
      right: 19px;
      top: 12px;
    }

    & p {
      user-select: none;
    }

    &.m-selected {
      & svg {
        display: block;
      }
    }

    &.m-checked {
      background-color: #f0f4ff;

      &:hover {
        background-color: #057dff;
      }
    }

    &.m-eror {
      color: #cd4e4e;
      &__text {
        color: #cd4e4e;
      }

      &:hover {
        background-color: #e64e4e;
        color: #fff;
      }

      &:active {
        background-color: #af4e4e;
      }
    }

    p {
      font-family: "Roboto", sans-serif;
      font-style: normal;
      font-weight: 400;
      font-size: 15px;
      line-height: 18px;
      margin: 0;
      transition: background-color 0.2s ease-out;
      user-select: none;
    }
  }
}
</style>
