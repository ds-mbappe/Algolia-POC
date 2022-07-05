<template>
  <ais-instant-search index-name="todos" :search-client="searchClient">
    <div class="video-bg">
      <video autoplay loop muted>
        <source
          src="https://assets.codepen.io/3364143/7btrrd.mp4"
          type="video/mp4"
        />
      </video>
    </div>
    <div class="left-panel">
      <h2>Brands</h2>
      <ais-refinement-list attribute="brand" show-more />
      <ais-configure :hitsPerPage="8" />
    </div>
    <div class="right-panel">
      <ais-search-box
        :class-names="{
          'ais-search-box': 'ais-search-box',
        }"
        placeholder="Search something here..."
      />
      <ais-hits
        :class-names="{
          'ais-Hits': 'MyHits',
          'ais-Hits-list': 'MyHitsList',
          'ais-Hits-item': 'MyHitsItem',
        }"
      >
        <template v-slot:item="{ item }">
          <div class="card-wrap">
            <div class="card" :style="cardStyle">
              <div class="card-bg" style="[cardBGTransform, cardBgImage]">
                <img
                  :src="
                    item.image['thumbnail']
                      ? item.image['thumbnail']
                      : 'https://freepngimg.com/thumb/categories/627.png'
                  "
                  align="left"
                  :alt="item.name"
                />
              </div>
              <div class="card-info">
                <h2>{{ item.name }}</h2>
              </div>
            </div>
          </div>
        </template>
      </ais-hits>
      <ais-pagination
        :show-first="false"
        :show-previous="false"
        :show-next="false"
        :show-last="false"
      />
    </div>
  </ais-instant-search>
</template>


<script>
import algoliasearch from "algoliasearch/lite";
//import "instantsearch.css/themes/satellite-min.css";

export default {
  props: ["dataImage"],
  data: () => ({
    searchClient: algoliasearch(
      process.env.VUE_APP_APP_ID,
      process.env.VUE_APP_API_KEY
    ),
  }),
  computed: {},
  methods: {},
};
</script>

<style>
body {
  font-family: sans-serif;
  background-image: url("https://assets.codepen.io/3364143/7btrrd.mp4");
}

.video-bg {
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  z-index: -5;
  width: 100%;
  height: 100%;
}

.video-bg video {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.left-panel {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 4em;
  margin-left: -1em;
}

.left-panel h2 {
  margin-left: 3em;
  color: white;
}

.ais-RefinementList-item--selected {
  color: rgb(241, 119, 119);
}

.ais-RefinementList-checkbox {
  border-radius: 50%;
}

.ais-RefinementList-label {
  width: 125%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.right-panel {
  margin-top: 4em;
  margin-right: 4em;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
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
  margin-top: 2em;
  border-radius: 0.5em;
  transition: 1s cubic-bezier(0.445, 0.05, 0.55, 0.95);
  transform: perspective(800px);
  transform-style: preserve-3d;
}

.card-wrap {
  margin: 10px;
  transition: 0.2s cubic-bezier(0.445, 0.05, 0.55, 0.95);
  cursor: pointer;
}

.card-wrap:hover {
  transform: scale(1.1);
}

.card-wrap:hover .card-info {
  transform: translateY(0);
}

.card-wrap:hover .card-info p {
  opacity: 1;
}

.card-wrap:hover .card-info,
.card-wrap:hover .card-info p {
  transition: 0.6s cubic-bezier(0.23, 1, 0.32, 1);
}

.card-wrap:hover .card-info:after {
  transition: 5s cubic-bezier(0.23, 1, 0.32, 1);
  opacity: 1;
  transform: translateY(0);
}

.card-wrap:hover .card-bg {
  transition: 0.6s cubic-bezier(0.23, 1, 0.32, 1),
    opacity 5s cubic-bezier(0.23, 1, 0.32, 1);
  opacity: 1;
}

.card-wrap:hover .card {
  transition: 0.6s cubic-bezier(0.23, 1, 0.32, 1),
    box-shadow 2s cubic-bezier(0.23, 1, 0.32, 1);
  box-shadow: rgba(255, 255, 255, 0.2) 0 0 10px 2px, white 0 0 0 1px,
    rgb(255, 255, 255) 0 10px 30px 0, inset rgb(255, 255, 255) 0 0 0 2px,
    inset white 0 0 0 2px;
}

.card {
  position: relative;
  flex: 0 0 240px;
  width: 240px;
  height: 320px;
  /* background-color: #333; */
  overflow: hidden;
  border-radius: 10px;
  box-shadow: rgba(255, 255, 255, 0.66) 0 10px 20px 0,
    inset rgb(255, 255, 255) 0 0 0 2px, inset rgba(255, 255, 255, 0.5) 0 0 0 2px;
  transition: 1s cubic-bezier(0.445, 0.05, 0.55, 0.95);
}

.card-bg {
  opacity: 1;
  position: absolute;
  top: -20px;
  left: -20px;
  width: 100%;
  height: 100%;
  padding: 20px;
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  transition: 1s cubic-bezier(0.445, 0.05, 0.55, 0.95),
    opacity 5s 1s cubic-bezier(0.445, 0.05, 0.55, 0.95);
  pointer-events: none;
}

.card-bg img {
  margin-top: 2em;
  width: 15em;
  height: 15em;
}

.card-info h2 {
  margin-top: 200px;
}

.card-info {
  padding: 20px;
  position: absolute;
  bottom: 0;
  color: #fff;
  transform: translateY(40%);
  transition: 0.6s 1.6s cubic-bezier(0.215, 0.61, 0.355, 1);
}
.card-info p {
  opacity: 0;
  text-shadow: black 0 2px 3px;
  transition: 0.6s 1.6s cubic-bezier(0.215, 0.61, 0.355, 1);
}
.card-info * {
  position: relative;
  z-index: 1;
}
.card-info:after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  z-index: 0;
  width: 100%;
  height: 100%;
  background-image: linear-gradient(
    to bottom,
    transparent 0%,
    rgba(0, 0, 0, 0.6) 100%
  );
  background-blend-mode: overlay;
  opacity: 0;
  transform: translateY(100%);
  transition: 5s 1s cubic-bezier(0.445, 0.05, 0.55, 0.95);
}

.card-info h1 {
  font-family: "Playfair Display";
  font-size: 36px;
  font-weight: 700;
  text-shadow: rgba(0, 0, 0, 0.5) 0 10px 10px;
}

.ais-RefinementList-list {
  list-style-type: none;
}

.ais-RefinementList-item {
  display: block;
  margin: 0.5em;
}

.ais-RefinementList-label {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  transition: 0.25s all ease-in-out;
}

.ais-RefinementList-label:hover {
  cursor: pointer;
  color: rgb(241, 119, 119);
  font-weight: bold;
  transform: scale(1.1);
}

.ais-RefinementList-count {
  background-color: rgb(227, 224, 224);
  border-radius: 5em;
  padding: 0.5em;
}

.ais-RefinementList-item--selected {
  font-weight: bold;
}

.ais-RefinementList-checkbox {
  width: 1em;
  height: 1em;
  border-radius: 50%;
}

.ais-RefinementList-showMore {
  display: none;
}

.ais-SearchBox-submit,
.ais-SearchBox-reset {
  display: none;
}

.ais-SearchBox-input {
  text-align: center;
  width: 50em;
  height: 3em;
  border-radius: 2.5em;
}

.ais-InstantSearch {
  display: grid;
  grid-template-columns: 1fr 4fr;
  grid-gap: 1em;
}

.hit-name {
  margin-bottom: 0.5em;
}

.hit-description {
  color: #888;
  font-size: 0.8em;
  margin-bottom: 0.5em;
}

.ais-Pagination-list {
  list-style-type: none;
  display: flex;
  flex-direction: row;
}

.ais-Pagination-item {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 2.5em;
  height: 2.5em;
  margin: 1em;
  border-radius: 50%;
  background-color: #000000;
  margin-top: 2em;
  margin-bottom: 2em;
  transition: 0.2s all ease-in-out;
}

.ais-Pagination-item:hover {
  transform: scale(1.25);
  cursor: pointer;
}

.ais-Pagination-link {
  text-decoration: none;
  font-size: 1.5em;
  color: white;
}

.ais-Pagination-item--selected {
  font-weight: bold;
  background-color: rgb(241, 119, 119);
}
</style>
