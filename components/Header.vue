<template>
  <div class="container">
    <h1>Add Favorite Book</h1>
    <form id="book-form">
      <div>
        <label for="title">Book</label>
        <input
          type="text"
          id="title"
          class="u-full-width"
          placeholder="Book name"
          v-model="title"
        />
      </div>
      <div>
        <label for="author">Author</label>
        <input
          type="text"
          id="author"
          class="u-full-width"
          placeholder="Author name"
          v-model="author"
        />
      </div>
      <div>
        <label for="released">Released</label>
        <input
          type="text"
          id="released"
          class="u-full-width"
          placeholder="Released date"
          v-model="released"
        />
      </div>
      <div>
        <button class="btn" @click.prevent="postData()">
          Add In Your list
        </button>
      </div>
    </form>

    <section class="table-section">
      <table>
        <tr id="table">
          <th>Book</th>
          <th>Author</th>
          <th>Released</th>
          <th>Update</th>
          <th>Delete</th>
        </tr>
        <tr v-for="item in items" :key="item.id">
          <td>{{ item.bookName }}</td>
          <td>{{ item.author }}</td>
          <td>{{ item.released }}</td>
          <td>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 30 30"
              width="30px"
              height="30px"
            >
              <path
                d="M 22.828125 3 C 22.316375 3 21.804562 3.1954375 21.414062 3.5859375 L 19 6 L 24 11 L 26.414062 8.5859375 C 27.195062 7.8049375 27.195062 6.5388125 26.414062 5.7578125 L 24.242188 3.5859375 C 23.851688 3.1954375 23.339875 3 22.828125 3 z M 17 8 L 5.2597656 19.740234 C 5.2597656 19.740234 6.1775313 19.658 6.5195312 20 C 6.8615312 20.342 6.58 22.58 7 23 C 7.42 23.42 9.6438906 23.124359 9.9628906 23.443359 C 10.281891 23.762359 10.259766 24.740234 10.259766 24.740234 L 22 13 L 17 8 z M 4 23 L 3.0566406 25.671875 A 1 1 0 0 0 3 26 A 1 1 0 0 0 4 27 A 1 1 0 0 0 4.328125 26.943359 A 1 1 0 0 0 4.3378906 26.939453 L 4.3632812 26.931641 A 1 1 0 0 0 4.3691406 26.927734 L 7 26 L 5.5 24.5 L 4 23 z"
              />
            </svg>
          </td>
          <td>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 30 30"
              width="30px"
              height="30px"
            >
              <path
                d="M 14.984375 2.4863281 A 1.0001 1.0001 0 0 0 14 3.5 L 14 4 L 8.5 4 A 1.0001 1.0001 0 0 0 7.4863281 5 L 6 5 A 1.0001 1.0001 0 1 0 6 7 L 24 7 A 1.0001 1.0001 0 1 0 24 5 L 22.513672 5 A 1.0001 1.0001 0 0 0 21.5 4 L 16 4 L 16 3.5 A 1.0001 1.0001 0 0 0 14.984375 2.4863281 z M 6 9 L 7.7929688 24.234375 C 7.9109687 25.241375 8.7633438 26 9.7773438 26 L 20.222656 26 C 21.236656 26 22.088031 25.241375 22.207031 24.234375 L 24 9 L 6 9 z"
              />
            </svg>
          </td>
        </tr>
      </table>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [],
      title: "",
      author: "",
      released: "",
    };
  },
  methods: {
    async getData() {
      let res = await this.$axios.get(
        "https://zany-rose-alligator-yoke.cyclic.app/todo/all"
      );
      this.items = res.data.todos;
      console.log(res.data.todos);
    },

    async postData() {
      try {
        const data = {
          bookName: this.title,
          author: this.author,
          released: this.released,
        };

        const response = await this.$axios.post(
          "https://zany-rose-alligator-yoke.cyclic.app/todo",
          data
        );
        return { response: data };
      } catch (error) {
        console.log(error);
      }
    },
  },
  mounted() {
    this.getData();
    this.postData();
  },
};
</script>

<style>
.container {
  background: #e8e8ec;
  align-items: center;
  justify-content: center;
  width: 1200px;
  margin: auto;
  box-sizing: border-box;
  padding: 0 10px;
  font-family: Arial, Helvetica, sans-serif;
  margin-top: -30px;
  padding: 5px 10px 35px 10px;
}
h1 {
  font-size: 2.3rem;
  font-weight: bold;
  color: #004b63;
}
#book-form {
  font-weight: bold;
  line-height: 1;
  font-size: 1.5rem;
  padding-bottom: 10px;
  color: #2479b3;
}
div {
  margin-top: 10px;
  padding: 5px 0;
}
/* input {
    width: 100%;
    margin: auto !important;
} */
/* .u-full-width {
  color: #a4bccb !important;
} */
div input {
  box-sizing: border-box;
  margin-top: 5px;
  border: 1px #96b2c0 solid;
  outline: none;
  border-radius: 7px;
  width: 100%;
  padding: 8px 15px;
}
.btn {
  font-weight: bold;
  font-size: 1.2rem;
  margin-top: 5px;
  border: 1px #96b2c0 solid;
  background: #68a0b5;
  color: white;
  border-radius: 7px;
  width: 100%;
  padding: 8px;
}

.btn:hover {
  background: #0b8ddd;
}

.table-section {
  display: grid;
}

.table-section tr {
  padding: 1rem;
  text-align: left;
}

.table-section td {
  padding: 0.5rem;
  margin-top: 1rem;
  font-size: 15px;
}

.table-section tr:nth-child(odd) {
  background: #68a0b5;
}

#table {
  background: #1b8fb4;
  height: 2rem;
  font-size: 20px;
}
</style>
