<template lang="html">
  <input type="tel"
         :value="formattedValue"
         v-on="listeners"
         v-money="{precision, decimal, thousands, prefix, suffix, allowBlank, min, max}"
         class="v-money" />
</template>

<script>
import money from "./directive";
import defaults from "./options";
import { format, unformat } from "./utils";

export default {
  name: "Money",
  props: {
    value: {
      required: true,
      type: [Number, String],
      default: 0
    },
    masked: {
      type: Boolean,
      default: false
    },
    precision: {
      type: Number,
      default: () => defaults.precision
    },
    decimal: {
      type: String,
      default: () => defaults.decimal
    },
    thousands: {
      type: String,
      default: () => defaults.thousands
    },
    prefix: {
      type: String,
      default: () => defaults.prefix
    },
    suffix: {
      type: String,
      default: () => defaults.suffix
    },
    allowBlank: {
      type: Boolean,
      default: () => defaults.allowBlank
    },
    min: {
      type: Number,
      default: () => defaults.min
    },
    max: {
      type: Number,
      default: () => defaults.max
    }
  },

  directives: { money },

  data() {
    return {
      formattedValue: ""
    };
  },

  computed: {
    listeners() {
      return {
        ...this.$listeners,
        change: this.change
      };
    }
  },

  watch: {
    value: {
      immediate: true,
      handler(newValue, oldValue) {
        var formatted = format(newValue, this.$props);
        if (formatted !== this.formattedValue) {
          this.formattedValue = formatted;
        }
      }
    }
  },

  methods: {
    change(evt) {
      this.$emit(
        "input",
        this.masked
          ? evt.target.value
          : unformat(evt.target.value, this.precision)
      );
    }
  }
};
</script>
