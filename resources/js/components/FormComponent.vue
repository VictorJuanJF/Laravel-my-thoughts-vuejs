<template>
  <div class="card">
    <div class="card-header">En que estas pensando ahora?</div>

    <div class="card-body">
      <!-- @if (session('status'))
            <div class="alert alert-success" role="alert">
                {{ session('status') }}
            </div>
      @endif-->
      <form v-on:submit.prevent="newThought()">
        <div class="form-group">
          <label for="thought">Ahora estoy pensando en:</label>
          <input
            type="text"
            class="form-control"
            name="thoguth"
            v-model="description"
            id="description"
          >
        </div>
        <input type="submit" class="btn btn-primary" value="Enviar pensamiento">
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      description: ""
    };
  },
  mounted() {
    console.log("Component mounted brus.");
  },
  methods: {
    newThought() {
      const params = {
        description: this.description
      };
      axios.post("/thoughts", params).then(response => {
        let thought = response.data;
        console.log("estoy enviando esto desde el componente form: ", thought);
        this.$emit("new-thought", thought);
        //   alert(description);
        this.description = "";
      });
    }
  }
};
</script>
