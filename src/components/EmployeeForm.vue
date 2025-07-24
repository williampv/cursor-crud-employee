<template>
  <div class="card mt-4">
    <div class="card-body">
      <h2 class="card-title mb-3">{{ props.employee ? 'Edit' : 'Add' }} Employee</h2>
      <form @submit="onSubmit">
        <div class="mb-3">
          <label for="firstName" class="form-label">First Name:</label>
          <input id="firstName" type="text" v-model="firstName" required class="form-control" />
        </div>
        <div class="mb-3">
          <label for="lastName" class="form-label">Last Name:</label>
          <input id="lastName" type="text" v-model="lastName" required class="form-control" />
        </div>
        <div class="mb-3">
          <label for="email" class="form-label">Email:</label>
          <input id="email" type="email" v-model="email" required class="form-control" />
        </div>
        <div class="mb-3">
          <label for="contactNo" class="form-label">Contact No:</label>
          <input id="contactNo" type="text" v-model="contactNo" required class="form-control" />
        </div>
        <div class="mb-3">
          <label for="city" class="form-label">City:</label>
          <input id="city" type="text" v-model="city" required class="form-control" />
        </div>
        <div class="mb-3">
          <label for="address" class="form-label">Address:</label>
          <input id="address" type="text" v-model="address" required class="form-control" />
        </div>
        <button type="submit" class="btn btn-success">Save</button>
      </form>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, watch, defineProps, defineEmits } from 'vue'

interface Employee {
  employeeId?: number
  firstName: string
  lastName: string
  email: string
  contactNo: string
  city: string
  address: string
}

const props = defineProps<{ employee?: Employee }>()
const emit = defineEmits(['save'])

const firstName = ref('')
const lastName = ref('')
const email = ref('')
const contactNo = ref('')
const city = ref('')
const address = ref('')

watch(() => props.employee, (newVal) => {
  if (newVal) {
    firstName.value = newVal.firstName
    lastName.value = newVal.lastName
    email.value = newVal.email
    contactNo.value = newVal.contactNo
    city.value = newVal.city
    address.value = newVal.address
  } else {
    firstName.value = ''
    lastName.value = ''
    email.value = ''
    contactNo.value = ''
    city.value = ''
    address.value = ''
  }
}, { immediate: true })

const onSubmit = (e: Event) => {
  e.preventDefault()
  emit('save', {
    employeeId: props.employee?.employeeId,
    firstName: firstName.value,
    lastName: lastName.value,
    email: email.value,
    contactNo: contactNo.value,
    city: city.value,
    address: address.value
  })
  firstName.value = ''
  lastName.value = ''
  email.value = ''
  contactNo.value = ''
  city.value = ''
  address.value = ''
}
</script> 