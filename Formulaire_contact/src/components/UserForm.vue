
<template>
    <div class="user-form-container">
      <h2>Formulaire Utilisateur</h2>
      <form @submit.prevent="submitForm">
        <div class="form-group">
          <label for="name">Nom :</label>
          <input type="text" id="name" v-model="form.name" />
          <span v-if="errors.name" class="error">{{ errors.name }}</span>
        </div>
        
        <div class="form-group">
          <label for="email">Email :</label>
          <input type="email" id="email" v-model="form.email" />
          <span v-if="errors.email" class="error">{{ errors.email }}</span>
        </div>
  
        <div class="form-group">
          <label for="phone">Téléphone :</label>
          <input type="text" id="phone" v-model="form.phone" />
          <span v-if="errors.phone" class="error">{{ errors.phone }}</span>
        </div>
  
        <button type="submit">Soumettre</button>
      </form>
  
      <div v-if="submitted" class="success-message">
        Formulaire soumis avec succès !
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        form: {
          name: '',
          email: '',
          phone: '',
        },
        errors: {},
        submitted: false,
      };
    },
    methods: {
      validateForm() {
        this.errors = {};
  
        
        if (!this.form.name) {
          this.errors.name = 'Le nom est requis.';
        }
  
        const emailPattern = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
        if (!this.form.email) {
          this.errors.email = "L'email est requis.";
        } else if (!emailPattern.test(this.form.email)) {
          this.errors.email = "L'email n'est pas valide.";
        }
  
       
        const phonePattern = /^\+?[1-9]\d{1,14}$/;
        if (!this.form.phone) {
          this.errors.phone = 'Le numéro de téléphone est requis.';
        } else if (!phonePattern.test(this.form.phone)) {
          this.errors.phone = 'Le numéro de téléphone n\'est pas valide.';
        }
  
        return Object.keys(this.errors).length === 0;
      },
      submitForm() {
        if (this.validateForm()) {
          this.submitted = true;
          console.log('Formulaire soumis avec succès', this.form);
        } else {
          this.submitted = false;
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .user-form-container {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    background-color: #f9f9f9;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  
  label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
  }
  
  input {
    width: 100%;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  
  .error {
    color: red;
    font-size: 14px;
    margin-top: 5px;
    display: block;
  }
  
  button {
    padding: 10px 15px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #0056b3;
  }
  
  .success-message {
    margin-top: 20px;
    color: green;
    font-weight: bold;
  }
  </style>
  