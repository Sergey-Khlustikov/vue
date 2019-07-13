<template>
  <div class="form-group"">
  <label>{{name}}
    <i class="fas" v-if="activated"
       :class="validClass"></i>
  </label>
  <input type="text" class="form-control"
         :value="value"
         @input="onInput"

  >
  </div>
</template>

<script>
    export default {
      props: ['name', 'value', 'pattern'],
      data() {
        return {
          activated: this.value != '',
        }
      },
      methods: {
        onInput(e) {
          this.activated = true;
          this.$emit('input', {
            value: e.target.value,
            valid: this.pattern.test(e.target.value),

          })

        }
      },
      computed: {
        validClass(){
          return this.pattern.test(this.value) ?
            'fa-check-circle text-success' :
            'fa-times-circle text-danger';
        },

      }
    }
</script>

