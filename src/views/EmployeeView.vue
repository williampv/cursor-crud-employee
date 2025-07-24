<template>
  <div class="container py-4">
    <h1 class="mb-4">Employee Management</h1>
    <EmployeeList
      @edit="editEmployee"
      @delete="deleteEmployee"
      :employees="employees"
    />
    <EmployeeForm
      :employee="editingEmployee"
      @save="addOrUpdateEmployee"
    />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import EmployeeList from '../components/EmployeeList.vue'
import EmployeeForm from '../components/EmployeeForm.vue'

interface Employee {
  employeeId: number
  firstName: string
  lastName: string
  email: string
  contactNo: string
  city: string
  address: string
}

const employees = ref<Employee[]>([])
const editingEmployee = ref<Employee | undefined>(undefined)

const fetchEmployees = async () => {
  const res = await fetch('http://localhost:8000/api/employees')
  employees.value = await res.json()
}

const addOrUpdateEmployee = async (employee: Partial<Employee>) => {
  if (employee.employeeId) {
    // Update
    await fetch(`http://localhost:8000/api/employees/${employee.employeeId}`, {
      method: 'PUT',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(employee)
    })
  } else {
    // Create
    await fetch('http://localhost:8000/api/employees', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(employee)
    })
  }
  editingEmployee.value = undefined
  await fetchEmployees()
}

const editEmployee = (employee: Employee) => {
  editingEmployee.value = { ...employee }
}

const deleteEmployee = async (employeeId: number) => {
  await fetch(`http://localhost:8000/api/employees/${employeeId}`, { method: 'DELETE' })
  await fetchEmployees()
}

fetchEmployees()
</script> 