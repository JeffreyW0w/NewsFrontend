<template>
  <div>
    <Label>Headline News</Label>
    <ul>
      <li>
        <News
          v-for="news in newsList"
          v-bind:key="news.description + news.author"
          v-bind:news="news"
        />
      </li>
    </ul>
  </div>
</template>
<script>
import axios from "axios";
import News from "@/components/News";
export default {
  name: "NewsList",
  props: ["msg"],
  data() {
    return {
      newsList: [],
    };
  },
  components: {
    News,
  },
  created() {
    axios
      .get("http://localhost:3000/news")
      .then((response) => {
        this.newsList = response.data.articles.filter((cur) => cur.description);
      })
      .catch((err) => {
        alert(err);
      });
  },
};
</script>

<style scoped>
label {
  display: block;
  height: 100%;
  font-size: 2.5rem;
  text-align: center;
  margin-bottom: 30px;
}

ul {
  list-style: none;
}
</style>
