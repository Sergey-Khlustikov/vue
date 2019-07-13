<template>
  <div id="app" class="wrapper">
    <form v-if="!show"  @submit.prevent="show = !show">

      <div class="progress" >
        <div class="progress-bar" :style="progressBar"></div>
      </div>
      <div>

        <app-input v-for="(el, index) in info"
                   :key="index"
                   :name="el.name"
                   :value="el.value"
                   :pattern="el.pattern"
                   @input="onInput(index, $event)"
        >
        </app-input>

      </div>
      <button class="btn btn-primary" :disabled="done < info.length">
        Send Data
      </button>

    </form>
    <div v-else>
      <table class="table table-bordered">
        <tr v-for="el in info">
          <td>{{el.name}}</td>
          <td>{{el.value}}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
  import AppInput from './components/AppInput.vue';
export default {
  components: {
    AppInput
  },
  beforeMount() {
    for(let i = 0; i < this.info.length; i++) {
      this.controls.push({
        validated: false,
      })
    }

  },
  data() {
    return {
      info: [
        {
          name: 'Name',
          value: '',
          pattern: /^[A-Za-z]{1,32}$/
        },
        {
          name: 'Phone',
          value: '',
          pattern: /^[0-9]{7,14}$/
        },
        {
          name: 'Email',
          value: '',
          pattern: /.+/
        },
        {
          name: 'Some Field 1',
          value: '',
          pattern: /.+/
        },
        {
          name: 'Some Field 2',
          value: '',
          pattern: /.+/
        }
      ],
      controls: [],
      show: false,
    }
  },
  methods: {
    onInput(index, data){
      this.info[index].value = data.value;
      this.controls[index].validated = data.valid;
    },
  },

  computed: {
    done() {
      let done = 0;
      for(let i = 0; i < this.controls.length; i++) {
        if(this.controls[i].validated) {
          done++;
        }
      }
      return done;
    },

    progressBar() {
      return {
        width: (this.done / this.info.length) * 100 +'%'
      }
    },


  }
}
</script>


