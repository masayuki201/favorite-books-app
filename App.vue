<template>
  <v-app>
    <HeaderBar
    @delete-local-storage="deleteLocalStorage"
    />
    <v-main>
      <v-container>
        <router-view
        :books="books"
        @add-book-list="addBook"
        @update-book-info="updateBookInfo"
        />
      </v-container>
    </v-main>
    <FooterBar/>
  </v-app>
</template>

<script>

import HeaderBar from "@/global/HeaderBar";
import FooterBar from "@/global/FooterBar";

const STORAGE_KEY = 'books'

export default {
  name: 'App',
  components: {
    FooterBar,
    HeaderBar,
  },
  data() {
    return {
      books: [],
      newBook: null,
    }
  },
  mounted() {
    if (localStorage.getItem(STORAGE_KEY)) {
      try {
        this.books = JSON.parse(localStorage.getItem(STORAGE_KEY));
      } catch (e) {
        localStorage.removeItem(STORAGE_KEY);
      }
    }
  },
  methods: {
    addBook(e) {
      this.books.push({
        id: this.books.length,
        title: e.title,
        image: e.image,
        description: e.description,
        readDate: '',
        memo: '',
      });
      this.saveBooks();
      //最後に追加したidの取得コード
      // console.log(this.books.slice(-1)[0].id)
      this.goToEditPage(this.books.slice(-1)[0].id)
    },
    removeBook(x) {
      this.books.splice(x, 1);
      this.saveBooks();
    },
    saveBooks() {
      const parsed = JSON.stringify(this.books);
      localStorage.setItem(STORAGE_KEY, parsed);
    },
    updateBookInfo(e){
      const updateInfo = {
        id: e.id,
        readDate: e.readDate,
        memo: e.memo,
        title: this.books[e.id].title,
        image: this.books[e.id].image,
        description: this.books[e.id].description,
      }
      this.books.splice(e.id, 1, updateInfo)
      this.saveBooks()
      this.$router.push('/')
    },
    goToEditPage(id){
      this.$router.push(`/edit/${id}`)
    },
    deleteLocalStorage(){
      const isDeleted = 'localstorageのデータを削除してもいいですか？'
      if(window.confirm(isDeleted)){
        localStorage.setItem(STORAGE_KEY, '');
        localStorage.removeItem(STORAGE_KEY)
        this.books = []
        window.location.reload()
      }
    }
  }
};
</script>
