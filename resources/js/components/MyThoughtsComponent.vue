<template>
  <div class="row justify-content-center">
    <div class="col-md-8">
      <form-component @new-thought="addThought($event)"></form-component>
      <thought-component
        v-for="(thought,index) in thoughts"
        :key="thought.id"
        :thought="thought"
        @update="updateThought(index,argument)"
        @delete="deleteThought(index)"
      ></thought-component>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      thoughts: []
    };
  },
  mounted() {
    axios.get("/thoughts").then(response => {
      this.thoughts = response.data;
    });
  },
  methods: {
    addThought(thought) {
      console.log(` me llego esto: ${thought}`);
      this.thoughts.push(thought);
    },
    deleteThought(index) {
      this.thoughts.splice(index, 1);
    },
    updateThought(index, thought) {
      this.thoughts[index] = thought;
    }
  }
};
</script>