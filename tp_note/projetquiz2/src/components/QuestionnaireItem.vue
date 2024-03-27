<script>

export default {
    props: {
        ma_tache:Object
    },
    data() {
        return {
        newIntitule: ''
        }
    },
    methods :{
      suppr: function (){
            this.$emit('remove',{id: this.ma_tache.id})
        },
      modif: function() {
          this.$emit('modify', {id:this.ma_tache.id, name:this.newIntitule});
          this.newIntitule = '';
      }
    },
    emits: ['remove', 'modify'],

}
</script>

<template>
  <li>
    <div class="checkbox">
        <label>
            <input type="checkbox" v-model="ma_tache.checked">
            {{ ma_tache.name }}
        </label>
        <input type = "text"
                placeholder="Modifier l'intitulé"
                v-model = "newIntitule"
                @keyup.enter="modif">
        <input type = "button" class = "btn btn-danger"
                value="Supprimer"
                @click= "suppr">
        <div class="alert alert-success" v-if="ma_tache.checked">
            Done
        </div>
    </div>
  </li>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>