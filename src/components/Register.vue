<template>
    <v-flex col-md-6 mt-16 offset-md-3>
        <v-form
            ref="form"
            v-model="valid"
            lazy-validation
            col-auto
            @submit.prevent="validate"
        >
            <v-text-field
            v-model="name"
            :counter="20"
            :rules="nameRules"
            label="Name"
            required
            ></v-text-field>

            <v-text-field
            v-model="email"
            :rules="emailRules"
            label="E-mail"
            required
            ></v-text-field>

            <v-text-field
            v-model="password"
            :rules="passRules"
            label="Password"
            hint="At least 8 characters"
            :append-icon="showpass ? 'mdi-eye' : 'mdi-eye-off'"
            :type="showpass ? 'text' : 'password'"
            counter
            @click:append="showpass = !showpass"
            required
            ></v-text-field>

            <v-select
            v-model="select"
            :items="items"
            :rules="[v => !!v || 'Gender is required']"
            label="Gender"
            required
            ></v-select>

            <v-btn
            :disabled="!valid"
            color="success"
            class="mr-4"
            @click="validate"
            >
            Submit
            </v-btn>

            <v-btn
            color="error"
            class="mr-4"
            @click="reset"
            >
            Reset Form
            </v-btn>
        </v-form>
    </v-flex>
</template>

<script>
  import axios from 'axios';

  export default {
    data: () => ({
      valid: true,
      name: '',
      nameRules: [
        v => !!v || 'Name is required',
        v => (v && v.length <= 20) || 'Name must be less than 20 characters',
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
      password: '',
      showpass: false,
      passRules: [
          v => !!v || 'Password is required',
          v => v.length >= 8 || 'Min 8 characters',
          v => /\d/.test(v) || 'Must have number',
          v => /[a-z]/.test(v) || 'Must have lowercase word',
          v => /[A-Z]/.test(v) || 'Must have uppercase word',
          v => /[!@#\$%\^\&*\)\(+=._-]/.test(v) || 'Must have special characters',
      ],
      select: null,
      items: [
        'Male',
        'Female',
        'Non Binary'
      ]
    }),

    methods: {
      async validate () {

        await axios.post('register', {
          name: this.name,
          email: this.email,
          password: this.password,
          select: this.select
        });   
        console.log(response)
        this.$router.push('/');
      },
      reset () {
        this.$refs.form.reset()
      },
      
    },


  }
</script>