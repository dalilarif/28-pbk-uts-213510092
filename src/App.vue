<template>
  <div class="todo-list">
    <h1>Aplikasi Booking Tiket Bioskop</h1>
    <form @submit.prevent="addTodo">
      <input type="text" v-model="newTodo" placeholder="Masukkan nama film..." required />
      <input type="text" v-model="newPeminjam" placeholder="Masukkan nama pemesan..." required />
      <input type="datetime-local" v-model="newDate" required />
      <select v-model="newRoom" required>
        <option disabled value="">Pilih ruangan</option>
        <option v-for="room in rooms" :key="room.id" :value="room.name">{{ room.name }}</option>
      </select>
      <button type="submit" class="tambahkan">Tambahkan</button>
    </form>
    <h2>List Item</h2>
    <div class="tengah">
      <ul>
        <li v-for="(todo, index) in todos" :key="index">
          <input type="checkbox" v-model="todo.done" />
          <span>{{ todo.text }}</span>
          <span>{{ todo.date }}</span>
          <span>{{ todo.room }}</span>
          <span :class="{ 'done': todo.done }">({{ todo.peminjam }})</span>
          <button @click="removeTodo(index)">Remove</button>
        </li>
      </ul>
      <div v-if="todos.length > 0">
        <button @click="removeAllTodos" class="remove-all">Remove All</button>
      </div>
    </div>
    <footer>
      <p>&copy;Dalil Arif Fadilah</p>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      newPeminjam: '',
      newDate: '',
      newRoom: '',
      todos: [],
      rooms: [
        { id: 1, name: 'Ruangan 1' },
        { id: 2, name: 'Ruangan 2' },
        { id: 3, name: 'Ruangan 3' },
      ],
    };
  },
  methods: {
    addTodo() {
      if (
        this.newTodo.trim().length === 0 ||
        this.newPeminjam.trim().length === 0 ||
        !this.newDate ||
        this.newRoom.trim().length === 0
      ) {
        return;
      }
      this.todos.push({
        text: this.newTodo,
        peminjam: this.newPeminjam,
        done: false,
        date: new Date(this.newDate).toLocaleString(),
        room: this.newRoom,
      });
      this.newTodo = '';
      this.newPeminjam = '';
      this.newDate = '';
      this.newRoom = '';
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    removeAllTodos() {
      this.todos = [];
    },
  },
};
</script>

<style>
h1{
  color: #fff;
}

h2{
  color: #fff;
}
  .todo-list {
    font-family: sans-serif;
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
  }
  body {
    background-image: url(https://cdnx.kincir.com/insecure/rs:fill:764:400/aHR0cHM6Ly9raW5jaXJpbWFnZS5zMy1hcC1zb3V0aGVhc3QtMS5hbWF6b25hd3MuY29tL3Byb2R1Y3Rpb24vMjAyMS0wOS9hdHVyYW4tbm9udG9uLWZpbG0tYmlvc2tvcC0xfjI5ZWI3MTNkLTYyMjgtNGZkYy05NzlhLTQ5OWIyMDljNmMzNC5qcGc=);
    background-size: cover;
  }
  .todo-list h1 {
text-align: center;
margin-bottom: 30px;
}

form {
display: flex;
flex-direction: column;
margin-bottom: 20px;
}

input[type='text'],
select,
input[type='datetime-local'] {
margin-bottom: 10px;
padding: 10px;
border-radius: 5px;
border: none;
font-size: 16px;
}

input[type='text']:focus,
select:focus,
input[type='datetime-local']:focus {
outline: none;
box-shadow: 0 0 5px 2px #5bc0de;
}

button[type='submit'] {
background-color: #5bc0de;
color: #fff;
border: none;
border-radius: 5px;
padding: 10px;
font-size: 16px;
cursor: pointer;
}

button[type='submit']:hover {
background-color: #31d570;
}

.tambahkan {
margin-top: 10px;
align-self: flex-end;
}

h2 {
margin-bottom: 10px;
}

ul {
list-style-type: none;
margin: 0;
padding: 0;
}

li {
display: flex;
align-items: center;
justify-content: space-between;
margin-bottom: 10px;
padding: 10px;
border-radius: 5px;
background-color: #fff;
box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
}

li.done {
background-color: #e6e6e6;
text-decoration: line-through;
}

input[type='checkbox'] {
margin-right: 10px;
cursor: pointer;
}

.remove-all {
background-color: #d9534f;
color: #fff;
border: none;
border-radius: 5px;
padding: 10px;
font-size: 16px;
cursor: pointer;
}

.remove-all:hover {
background-color: #c9302c;
}

.tengah {
display: flex;
flex-direction: column;
justify-content: center;
align-items: center;
}

footer {
margin-top: 20px;
text-align: center;
font-size: 14px;
}

footer p {
margin: 0;
padding: 0;
color: #fff;
}
</style>