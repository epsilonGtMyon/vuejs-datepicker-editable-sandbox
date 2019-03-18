<template>
  <Datepicker
    ref="datepicker"
    v-model="computedValue"
    class="my-date-picker"
    format="yyyy/MM/dd"
    :language="language"
  >
    <input
      type="text"
      v-model="internalValue"
      slot="afterDateInput"
      maxlength="10"
      @blur="onBlurInput"
      @click="clickInput"
    >
  </Datepicker>
</template>

<script>
import Datepicker from "vuejs-datepicker";
import { ja } from "vuejs-datepicker/dist/locale";

function format(d) {
  if (d === null || d === undefined || d === "") {
    return null;
  }
  const year = d.getFullYear();
  const month = d.getMonth() + 1;
  const day = d.getDate();

  return `${year}/${("0" + month).slice(-2)}/${("0" + day).slice(-2)}`;
}

export default {
  name: "EditableDatePicker",
  components: {
    Datepicker
  },
  props: {
    value: {
      required: true
    }
  },
  data() {
    return {
      language: ja,
      internalValue: null
    };
  },
  watch: {
    value(nVal, oVal) {
      this.internalValue = nVal;
    },
    internalValue(nVal, oVal) {
      this.$emit("input", nVal);
    }
  },
  methods: {
    onBlurInput() {
      this.closeCalendar();
    },
    clickInput() {
      this.showCalendar();
    },
    showCalendar() {
      this.$refs.datepicker.showCalendar();
    },
    closeCalendar() {
      this.$refs.datepicker.close();
    }
  },
  computed: {
    computedValue: {
      get() {
        return this.internalValue;
      },
      set(val) {
        this.internalValue = format(val);
        this.$emit("input", this.internalValue);
      }
    }
  }
};
</script>

<style lang="scss">
.my-date-picker {
  input[readonly] {
    display: none;
  }
  .weekend {
    &.sat {
      color: blue;
    }
    &.sun {
      color: red;
    }
  }
}
</style>
