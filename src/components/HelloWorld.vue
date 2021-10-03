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
            v-model="email"
            :rules="emailRules"
            label="E-mail"
            required
            ></v-text-field>

            <v-text-field
            v-model="password"
            label="Password"
            hint="At least 8 characters"
            :append-icon="showpass ? 'mdi-eye' : 'mdi-eye-off'"
            :type="showpass ? 'text' : 'password'"
            @click:append="showpass = !showpass"
            required
            ></v-text-field>

            <v-btn
            :disabled="!valid"
            color="success"
            class="mr-4"
            @click="validate"
            >
            Login
            </v-btn>

        </v-form>
    </v-flex>
</template>

<script>
import axios from 'axios';

export default {
    data(){
      return {
        email: '',
        password: '',
        emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
        ],
      showpass: false,
      passRules: [
          v => !!v || 'Password is required',
          v => v.length >= 8 || 'Min 8 characters',
          v => /\d/.test(v) || 'Must have number',
          v => /[a-z]/.test(v) || 'Must have lowercase word',
          v => /[A-Z]/.test(v) || 'Must have uppercase word',
          v => /[!@#\$%\^\&*\)\(+=._-]/.test(v) || 'Must have special characters',
      ]
      }
    },

    methods: {
     async validate() {
        const response = await axios.post('login',{
          email: this.email,
          password: this.password
        });

        console.log(response);
      }
    },

 }
</script>