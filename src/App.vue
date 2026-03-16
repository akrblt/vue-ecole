<script setup>

import { ref, watch } from 'vue';

import StudentList from './components/StudentList.vue';
import Studentform from './components/studentform.vue';



const STORAGE_KEY = 'vue-ecole-students'

const students = ref(JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]'))


function addStudent(student) {
  students.value.push(student)
}

watch(students , (newVal) => {
  localStorage.setItem(STORAGE_KEY,JSON.stringify(newVal))
},{deep: true})

</script>

<template>
   <div class="container mt-5 ">
    <h1 class="mb-4 text-center"> <strong>Liste des etudiants</strong></h1>
    <div class="row mb-4">
      
        <StudentList :students="students" />
      
      </div>

      <div class="row">

        <h2 class="mb-4 text-center"><strong>Formulaire d'inscription</strong></h2>
      
      <div class="col-12">
        <Studentform @student-added="addStudent" />
      </div>
      </div>

      <hr>
    
   
  </div>
</template>