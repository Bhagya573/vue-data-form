<template>
  <div class="form-container">
    <h3 class="form-title">Form Data</h3>
    <form @submit.prevent="submitForm">
      <div class="form-group">
        <label for="name">Name:</label>
        <input
          v-model="name"
          type="text"
          id="name"
          placeholder="Enter name"
          :class="{'input-error': errors.name}"
        />
        <div v-if="nameError" class="error-message">{{ nameError }}</div>
      </div>

      <div class="form-group">
        <label for="age">Age:</label>
        <input
          v-model="age"
          type="number"
          id="age"
          placeholder="Enter age"
          :class="{'input-error': errors.age}"
        />
        <div v-if="ageError" class="error-message">{{ ageError }}</div>
      </div>

      <button
        type="submit"
        class="submit-button"
      >
        Add Item
      </button>
    </form>
  </div>
</template>

<script>
import { useForm, useField } from 'vee-validate'; 
import * as yup from 'yup'; 

export default {
  name: 'FormComponent',
  setup(props, { emit }) {
    // Validation schema using Yup
    const validationSchema = yup.object({
      name: yup.string().required('Name is required!'),
      age: yup
        .number()
        .positive('Age must be a positive number!')
        .required('Age is required!')
        .integer('Age must be a valid integer!'),
    });

    // Using useForm for managing form state and validation
    const { handleSubmit, errors, resetForm } = useForm({
      validationSchema,
    });

    // Using useField for each individual field
    const { value: name, errorMessage: nameError } = useField('name');
    const { value: age, errorMessage: ageError } = useField('age');

    // Submit handler
    const submitForm = handleSubmit((values) => {
      console.log("submit form")
      const newItem = {
        name: values.name,
        age: values.age,
      };

      // Emit item to the parent component
      emit('add-item', newItem);

      // Reset the form
      resetForm();
    });
    return {
      name,
      age,
      errors,
      nameError,
      ageError,
      submitForm
    };
  },
};
</script>
