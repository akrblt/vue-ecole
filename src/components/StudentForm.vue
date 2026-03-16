<script setup>
    import { computed, reactive, ref } from 'vue';

    const emit =defineEmits(["student-added"])

    const INTEREST_OPTIONS = [
        'Sport',
        'Environnement',
        'Science',
        'Tecnology',
        'News'
    ]

    const form = reactive({
        name: '',
        surname:'',
        birth:'',
        gender: 'Male' , // Male , Female, Other
        mood: 50,
        motivation: '',
        interests: []

    })

    function getEmojiByMood(mood) {
  // orijinal fonksiyona benzer, mood 0-100 aralığında
  const emojis = ["😢", "😁", "😊", "😒", "😃", "😐", "😖", "😤", "😟", "😆"]
  let index = Math.floor(mood / 10) - 1
  if (index < 0) index = 0
  if (index >= emojis.length) index = emojis.length - 1
  return emojis[index]
}

const emoji = computed(() => getEmojiByMood(form.mood))
function toggleInterest(option) {
  const idx = form.interests.indexOf(option)
  if (idx === -1) form.interests.push(option)
  else form.interests.splice(idx, 1)
}

function validate() {
  if (!form.name.trim() || !form.surname.trim()) {
    alert('Svp saisir votre prenom et nom')
    return false
  }
  if (!form.birth) {
    alert('Svp saisir votre date de naissance')
    return false
  }
  if (!form.motivation.trim()) {
    alert('Svp saisir votre motivation')
    return false
  }
  return true
}

function onSubmit() {
  if (!validate()) return

  const student = {
    id: Date.now(),
    name: form.name.trim(),
    surname: form.surname.trim(),
    birth: form.birth,
    gender: form.gender,
    mood: form.mood,
    emoji: emoji.value,
    motivation: form.motivation.trim(),
    interests: [...form.interests]
  }

  emit('student-added', student)

  // supprimer les donnes de form
  form.name = ''
  form.surname = ''
  form.birth = ''
  form.gender = 'Male'
  form.mood = 50
  form.motivation = ''
  form.interests = []
}



    //const name =ref("")
   // const surname =ref("")

  /*  function submitForm(){
        if(!name.value || !surname.value) {
            alert(" Toutes les champes obligatoires")
            return
        }

        const student = {
            name :name.value,
            surname :surname.value

        }

        emit("student-added",student)
        name.value = ""
        surname.value=""
    } */



</script>

<template>
    <form class="card p-3 " @submit.prevent="onSubmit">
        <h3 class="mb-3">Ajouter un etudiant</h3>

        <div class="mb-2">
            <label class="form-label">Nom</label>
            <input class="form-control" v-model="form.surname" placeholder="Nom">

        </div>

        <div class="mb-2">
            <label class="form-label">Prenom</label>
            <input class="form-control" v-model="form.name" placeholder="Prenom">
         </div>

          <div class="mb-2">
      <label class="form-label">Date de naissance</label>
      <input class="form-control" type="date" v-model="form.birth">
    </div>

    <div class="mb-3">
      <label class="form-label d-block">Genre</label>
      <div class="form-check form-check-inline" v-for="g in ['Male','Female','Other']" :key="g">
        <input class="form-check-input" type="radio" :id="'g-'+g" v-model="form.gender" :value="g">
        <label class="form-check-label" :for="'g-'+g">{{ g }}</label>
      </div>
    </div>

    <div class="mb-3">
      <label class="form-label d-block">Caractère (mood): <span class="fw-bold">{{ form.mood }}</span> <span style="font-size:1.4rem">{{ emoji }}</span></label>
      <input type="range" min="0" max="100" v-model.number="form.mood" class="form-range">
    </div>

    <div class="mb-3">
      <label class="form-label">Motivation</label>
      <textarea class="form-control" rows="3" v-model="form.motivation"></textarea>
    </div>

    <div class="mb-3">
  <label class="form-label d-block">Centres d'intérêts</label>

  <div class="form-check" v-for="option in INTEREST_OPTIONS" :key="option">
    <input
      class="form-check-input"
      type="checkbox"
      :id="option"
      :value="option"
      v-model="form.interests"
    >
    <label class="form-check-label" :for="option">
      {{ option }}
    </label>
  </div>
</div>

    <div class="d-flex justify-content-center">
      <button type="submit" class="btn btn-success">Soumettre</button>
      <hr/>
      
    </div>


   
    </form>


</template>