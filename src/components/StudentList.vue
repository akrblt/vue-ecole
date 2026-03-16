 <script setup>



import { computed } from 'vue'

const props = defineProps({
  students: {
    type: Array,
    required: true
  }
})

/*
function formatDate(iso) {
  if(!iso) return ''
  const d = new Date(iso)
  return d.toLocaleDateString()
}

function calculateAge(iso) {
  if (!iso) return ''
  const b = new Date(iso)
  const now = new Date()
  let age = now.getFullYear() - b.getFullYear()
  const m = now.getMonth() - b.getMonth()
  if (m < 0 || (m === 0 && now.getDate() < b.getDate())) age--
  return age
}
  */

</script>

<template>
  <div class="row">
    <div class="col-md-4 mb-5" v-for="student in students" :key="student.id">
      <div class="card h-100">
        <div class="card-body">
          <h5 class="card-title">{{ student.name }} {{ student.surname }}</h5>
          <p><strong>Description : </strong>{{ student.motivation }}</p>
          <p><strong>Genre : </strong> {{ student.gender }}</p>
          <p><strong>Centres d'interêts: </strong>{{ student.interests.join(', ') || '—' }}</p>
          <p><strong>Date de naissance : </strong> {{ student.birth }}</p>
          <p><strong>Caractere : </strong>{{ student.emoji }}</p>
          <p><strong>photo :</strong> </p>
          
          
          
        </div>
      </div>
    </div>
  </div>
</template>


<style scoped>
.card-title { margin-bottom: .25rem; }
</style>
