<template>
  <div id="app">
    <h1>Cadastro de Livros</h1>

    <!-- Formulário de cadastro -->
    <form @submit.prevent="addBook">
      <div>
        <label for="title">Título:</label>
        <input type="text" v-model="newBook.title" required />
      </div>
      <div>
        <label for="author">Autor:</label>
        <input type="text" v-model="newBook.author" required />
      </div>
      <div>
        <label for="price">Preço:</label>
        <input type="number" v-model="newBook.price" required min="0" step="0.01" />
      </div>
      <button type="submit">Cadastrar Livro</button>
    </form>

    <!-- Lista de livros -->
    <div v-if="books.length > 0">
      <h2>Lista de Livros</h2>
      <ul>
        <li v-for="(book, index) in books" :key="index">
          <p><strong>Título:</strong> {{ book.title }}</p>
          <p><strong>Autor:</strong> {{ book.author }}</p>
          <p><strong>Preço:</strong> R$ {{ book.price.toFixed(2) }}</p>
          <button @click="deleteBook(index)">Deletar</button>
        </li>
      </ul>
    </div>
    <p v-else>Nenhum livro cadastrado.</p>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "App",
  setup() {
    const newBook = ref({
      title: "",
      author: "",
      price: null,
    });

    const books = ref([]);

    const addBook = () => {
      if (newBook.value.title && newBook.value.author && newBook.value.price !== null) {
        books.value.push({ ...newBook.value });
        newBook.value.title = "";
        newBook.value.author = "";
        newBook.value.price = null;
      }
    };

    const deleteBook = (index) => {
      books.value.splice(index, 1);
    };

    return {
      newBook,
      books,
      addBook,
      deleteBook,
    };
  },
};
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}

form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

form div {
  margin-bottom: 10px;
}

button {
  margin-top: 10px;
}

ul {
  list-style-type: none;
  padding: 0;
}
</style>
