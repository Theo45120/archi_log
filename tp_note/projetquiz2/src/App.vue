<script setup>
import QuestionnaireItem from './components/QuestionnaireItem.vue';
</script>

<script>

let data = {
        questionnaires: [
        ],
        title: 'Mes Questionnaires: ',
        newQuestionnaire: ''
    }

export default {
  data () {
    return data;
  },
  methods: {
    addquestionnaire: function(){
      if(this.newQuestionnaire){
        this.questionnaires.push({ id: this.questionnaires.length + 1, name: this.newQuestionnaire, checked: false })
      }
        this.newQuestionnaire = ''
    },
    removeItem($event) {
        this.questionnaires = this.questionnaires.filter(questionnaire => questionnaire.id !== $event.id);
    },
    modifyItem($event){
        let index = this.questionnaires.findIndex(questionnaire => questionnaire.id === $event.id);
        if(index !== -1){
          this.questionnaires[index].name = $event.name;
    }
  }
  },
  mounted(){
                    fetch('http://127.0.0.1:5000/quiz/api/v1.0/quiz')
                    .then(response => response.json())
                    .then(json => {
                        this.questionnaires = json
                    })
                },
  components: { QuestionnaireItem }
}

</script>

<template>
  <link rel="stylesheet"
            href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css"
            integrity ="sha384-rbsA2VBKQhggwzxH7pPCaAqO46MgnOM80zW1RWuH61DGLwZJEdK2Kadq2F9CUG65"
            crossorigin ="anonymous">
  <div id="app" class="container">
            <h2>{{ title }}</h2>
            <ol>
                <QuestionnaireItem @remove="removeItem" @modify="modifyItem" v-for="questionnaire in questionnaires" :ma_tache='questionnaire' v-bind:class ="{ 'alert alert-success': questionnaire.checked }"></QuestionnaireItem>
            </ol>
            <div class="container">
                <h2> Ajouter un Questionnaire</h2>
                <input v-model ="newQuestionnaire" type="text" @keyup.enter="addquestionnaire()" />
                <span class="input-group-btn">
                    <button v-on:click ="addquestionnaire()"
                        class="btn btn-default"
                        type="button">
                        Ajouter un Questionnaire
                    </button>
                </span>
            </div>
        </div>
</template>