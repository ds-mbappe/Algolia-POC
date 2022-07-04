<template>
  <ais-instant-search index-name="todos" :search-client="searchClient">
    <div class="left-panel">
      <ais-clear-refinements />
      <h2>Brands</h2>
      <ais-refinement-list attribute="brand" searchable show-more />
      <ais-configure :hitsPerPage="8" />
    </div>
    <div class="right-panel">
      <ais-search-box />
      <ais-hits
        :class-names="{
          'ais-Hits': 'MyHits',
          'ais-Hits-list': 'MyHitsList',
          'ais-Hits-item': 'MyHitsItem',
        }"
      >
        <template v-slot:item="{ item }">
          <img
            :src="
              item.image['thumbnail']
                ? item.image['thumbnail']
                : 'https://freepngimg.com/thumb/categories/627.png'
            "
            align="left"
            :alt="item.name"
          />
          <h2>{{ item.name }}</h2>
          <!-- <div class="hit-name">
            <ais-highlight attribute="name" :hit="item"></ais-highlight>
          </div>
          <div class="hit-description">
            <ais-highlight attribute="description" :hit="item"></ais-highlight>
          </div>
          <div class="hit-price">{{ item.retailPrice }}</div> -->
        </template>
      </ais-hits>
      <ais-pagination />
    </div>
  </ais-instant-search>
</template>


<script>
import algoliasearch from "algoliasearch/lite";
import "instantsearch.css/themes/satellite-min.css";

export default {
  data() {
    return {
      searchClient: algoliasearch(
        "YJHN654C85",
        "9b84d059dbc4a12bd5822bf49da269f6"
      ),
    };
  },
};

const wrapper = document.getElementsByName(".MyHits");

wrapper.forEach((element) => {
  let state = {
    mouseX: 0,
    mouseY: 0,
    height: element.clientHeight,
    width: element.clientWidth,
  };

  element.addEventListener("mousemove", (ele) => {
    const card = element.querySelector(".MyHitsItem");
    state.mouseX = ele.pageX - element.offsetLeft - state.width / 2;
    state.mouseY = ele.pageY - element.offsetTop - state.height / 2;

    // angle in card
    const angleX = (state.mouseX / state.width) * 30;
    const angleY = (state.mouseY / state.height) * -30;
    card.style.transform = `rotateY(${angleX}deg) rotateX(${angleY}deg) `;
  });

  element.addEventListener("mouseout", () => {
    const card = element.querySelector(".MyHitsItem");
    card.style.transform = `rotateY(0deg) rotateX(0deg) `;
  });
});
</script>

<style>
body {
  font-family: sans-serif;
  padding: 1em;
}

.MyHits {
  margin-top: 2em;
  display: flex;
  justify-content: center;
  align-items: center;
  transform: perspective(800px);
  transform-style: preserve-3d;
  cursor: pointer;
}

.MyHitsItem:hover {
  transform: scale(1.1);
  transition: 0.6s cubic-bezier(0.23, 1, 0.32, 1),
    box-shadow 2s cubic-bezier(0.23, 1, 0.32, 1);
  box-shadow: rgba(225, 225, 225, 0.2) 0 0 40px 5px, white 0 0 0 1px,
    rgba(0, 0, 0, 0.66) 0 5px 10px 0;
}

.MyHitsList {
  display: grid;
  gap: 2em;
  grid-template-rows: repeat(2, 22em);
  grid-template-columns: repeat(4, 15em);
  margin-top: 0;
  margin-bottom: 1em;
}

.MyHitsItem {
  position: relative;
  display: flex;
  flex-direction: column;
  border-radius: 0.5em;
  transition: 1s cubic-bezier(0.445, 0.05, 0.55, 0.95);
}

.ais-InstantSearch {
  display: grid;
  grid-template-columns: 1fr 4fr;
  grid-gap: 1em;
}

.MyHitsItem img {
  width: 15em;
  height: 15em;
  margin-right: 1em;
}
.hit-name {
  margin-bottom: 0.5em;
}
.hit-description {
  color: #888;
  font-size: 0.8em;
  margin-bottom: 0.5em;
}
</style>
