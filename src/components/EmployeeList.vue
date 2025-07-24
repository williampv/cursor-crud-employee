<template>
  <div>
    <h2>Employees</h2>
    <table class="table table-striped table-bordered">
      <thead class="thead-dark">
        <tr>
          <th>ID</th>
          <th>First Name</th>
          <th>Last Name</th>
          <th>Email</th>
          <th>Contact No</th>
          <th>City</th>
          <th>Address</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="employee in props.employees" :key="employee.employeeId">
          <td>{{ employee.employeeId }}</td>
          <td>{{ employee.firstName }}</td>
          <td>{{ employee.lastName }}</td>
          <td>{{ employee.email }}</td>
          <td>{{ employee.contactNo }}</td>
          <td>{{ employee.city }}</td>
          <td>{{ employee.address }}</td>
          <td>
            <button class="btn btn-primary btn-sm me-2" @click="$emit('edit', employee)">Edit</button>
            <button class="btn btn-danger btn-sm" @click="$emit('delete', employee.employeeId)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits } from 'vue'

interface Employee {
  employeeId: number
  firstName: string
  lastName: string
  email: string
  contactNo: string
  city: string
  address: string
}

const props = defineProps<{ employees: Employee[] }>()
const emit = defineEmits(['edit', 'delete'])
</script> 