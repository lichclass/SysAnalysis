<template>
  <b-container class="bv-example-row">
    <b-row>
      <b-col></b-col>
      <b-col>
        <div>
          <b-form @submit="onSubmit" @reset="onReset" v-if="show">
            <b-form-group
              id="input-group-1"
              label="Email address:"
              label-for="input-1"
            >
              <b-form-input
                id="input-1"
                v-model="form.email"
                type="email"
                placeholder="Enter email"
                required
              ></b-form-input>
            </b-form-group>
            <b-form-group
              id="input-group-1"
              label="Password:"
              label-for="input-1"
            >
              <b-form-input
                id="input-1"
                v-model="form.password"
                type="password"
                placeholder="Enter password"
                required
              ></b-form-input>
            </b-form-group>

            <div class="d-flex justify-content-center">
              <b-button type="button" variant="primary" @click="register()">Sign-up</b-button>
            </div>
            
          </b-form>
          
        </div>
      </b-col>
      <b-col></b-col>
    </b-row>
  </b-container>
</template>

<script>
import axios from 'axios';

  export default {
    data() {
      return {
        form: {
          email: '',
          password: ''
        },
        show: true
      }
    },
    methods: {
      register() {
        axios.post('/register/registration', this.form).then(response=>{
          console.log(response.data.email);
          console.log(response.data.password);
        }).catch(error=>{
          console.log(error.data);
          this.loading = false;
        })
      },
      onSubmit(event) {
        event.preventDefault()
        // alert(JSON.stringify(this.form))
      },
      onReset(event) {
        event.preventDefault()
        // Reset our form values
        this.form.email = ''
        this.form.password = ''
        this.form.food = null
        this.form.checked = []
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      }
    }
  }
</script>