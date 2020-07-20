<template>
  <li>
    <h4 class="news-wrapper" @click="expand">
      {{ news.description }}
    </h4>
    <br />
    <div
      class="source-wrapper"
      v-if="expandStatus && news.source.name && news.author"
    >
      <label class="source"> {{ news.source.name }},</label>
      <label class="author">
        {{ news.author }}
      </label>
      <br />
      <label class="date" v-if="news.publishedAt">
        {{
          news.publishedAt
            .split("T")
            .reduce((prev, cur) => (prev += " " + cur))
            .slice(0, -4)
        }}
      </label>
      <a :href="news.url" class="url">
        {{ news.url }}
      </a>
    </div>
    <div class="content-wrapper" v-if="expandStatus">
      <label v-if="expandStatus" class="content">
        {{ news.content }}
      </label>
      <button v-if="expandStatus" @click="save">Save For Later</button>
      <button v-if="expandStatus" @click="collapse">Collapse</button>
    </div>
  </li>
</template>

<script>
import axios from "axios";
export default {
  name: "News.vue",
  props: ["news"],
  data: function () {
    return {
      expandStatus: false,
    };
  },
  methods: {
    expand() {
      this.expandStatus = !this.expandStatus;
    },
    collapse() {
      this.expandStatus = false;
    },
    save() {
      axios
        .post("http://localhost:3000/news/save", {
          title: this.news.description,
          url: this.news.url,
        })
        .then(() => {
          this.expandStatus = false;
        })
        .catch((err) => {
          alert(err);
        });
    },
  },
};
</script>

<style scoped>
h4 {
  width: 100%;
  font-weight: bold;
}

li {
  margin: 10px 20%;
  padding: 20px 5%;
  background-color: #2c3e50;
  user-select: none;
}
.news-wrapper {
  display: block;
  color: white;
  font-size: 1.2rem;
}

.content {
  display: block;
  color: white;
  font-size: 1rem;
  margin-top: 10px;
  line-height: 2rem;
}

.source,
.author,
.date,
.url {
  display: inline-block;
  color: lightgray;
  font-size: 1rem;
  margin: 5px;
}

h4:hover,
button:hover {
  cursor: pointer;
}

li:hover {
  background-color: teal;
}

button:hover {
  background-color: darkslategray !important;
}

button {
  height: 10%;
  width: 100%;
  margin: 10px 10px;
  padding: 10px;
  background-color: transparent;
  border: 1px solid white;
  color: white;
}
</style>
