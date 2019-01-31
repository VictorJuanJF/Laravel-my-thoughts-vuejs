<template>
  <div class="card">
    <div
      class="card-header"
    >{{thought.id}}. Publicado en {{thought.created_at}} - Ultima actualizacion: {{thought.updated_at}}</div>
    <div class="card-body">
      <input v-if="editMode" type="text" name id class="form-control" v-model="thought.description">
      <p v-else class="card-text">{{thought.description}}</p>
    </div>
    <div class="card-footer text-muted">
      <button v-if="editMode" class="btn btn-success" v-on:click="onClickUpdate()">Guardar Cambios</button>
      <button v-else class="btn btn-default" v-on:click="onClickEdit()">Editar</button>
      <button class="btn btn-danger" v-on:click="onClickDelete()">Eliminar</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["thought"],
  data() {
    return {
      editMode: false
    };
  },
  mounted() {
    console.log("Component mounted brus.");
  },
  methods: {
    onClickDelete() {
      console.log("te pica? checa: ", this.thought.id);
      axios.delete(`/thoughts/${this.thought.id}`).then(() => {
        this.$emit("delete");
      });
    },
    onClickEdit() {
      this.editMode = true;
    },
    onClickUpdate() {
      let params = {
        description: this.thought.description
      };
      axios.put(`/thoughts/${this.thought.id}`, params).then(response => {
        this.editMode = false;
        let thought = response.data;
        this.$emit("update", thought);
      });
    }
  }
};
</script>
