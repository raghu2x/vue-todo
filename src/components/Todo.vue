<template>
  <b-container class="p-3">
    <b-row class="flex-nowrap gap-3 p-3">
      <b-form-input class="w-25 flex-grow-1" type="text" v-model="newtodo" maxlength="30" placeholder="ex:- learn vue js" />
      <b-button class="w-25" variant="success" size="sm" @click="addTodo"> Add </b-button>
      <!-- <b-form-input class="w-25 flex-grow-1" type="text" v-model="filtertodo" maxlength="30" placeholder="filter todolist" /> -->
    </b-row>

    <b-list-group>
      <b-list-group-item class="bg-primary text-white my-2 rounded py-2 px-3 d-flex align-items-center justify-content-between" v-for="list in filtered" :key="list.id">
        {{ list.text }}
        <b-button size="sm" @click="removetodo(list.id)" variant="danger"> Delete </b-button>
      </b-list-group-item>
    </b-list-group>
  </b-container>
</template>

<script>
let id = 0;
export default {
  data() {
    return {
      newtodo: '',
      filtertodo: '',
      todolist: [
        { id: id++, text: 'learn javascript' },
        { id: id++, text: 'learn vue.js' },
      ],
    };
  },
  computed: {
    filtered() {
      return this.todolist.filter((i) => {
        return i.text.toLowerCase().includes(this.filtertodo.toLowerCase());
      });
    },
  },
  methods: {
    addTodo() {
      if (this.newtodo.length > 0) {
        this.todolist.push({ id: id++, text: this.newtodo });
        this.newtodo = '';
      }
    },
    removetodo(i) {
      this.todolist = this.todolist.filter((v) => v.id !== i);
    },
  },
};
</script>
