<template>
  <div ref="scrollList">
    <ListItem
      v-for="(content, index) in contents"
      :key="index"
      :content="content"
    />
  </div>
</template>

<script>
import { ref } from "@vue/reactivity";
import ListItem from "./Item.vue";
import { onMounted } from "@vue/runtime-core";

export default {
  name: "MainList",
  components: {
    ListItem,
  },
  setup() {
    let page = 1;
    let contents = ref([]);
    const scrollList = ref(null);

    onMounted(() => {
      window.addEventListener("scroll", scrollEventHandle);
    });

    const getMoreContents = (number) => {
      page += 1;
      getContents(page, number);
    };

    const scrollEventHandle = () => {
      let element = scrollList.value;
      if (element.getBoundingClientRect().bottom < window.innerHeight) {
        getMoreContents(6);
      }
    };

    const getContents = (page, number) => {
      fetch(
        "https://api.github.com/users/grokify/repos?per_page=" +
          number +
          "&page=" +
          page
      )
        .then((response) => response.json())
        .then((data) => {
          data.forEach((f) => {
            contents.value.push(f);
          });
        })
        .catch((err) => console.log(err));
    };

    getContents(page, 6);

    return {
      contents,
      scrollList,
    };
  },
};
</script>
