<template>
  <div>
    <div v-if="step == 0">
      <Post :postData="postData[i]" v-for="(a, i) in postData" :key="i" />
    </div>

    <div v-if="step == 1">
      <div class="upload-image" :style="`background-image:url(${image})`"></div>
      <div class="filters">
        <FilterBox :filter="filter" :image="image" v-for="filter in instagramFilter" :key="filter">
          {{filter}}
        </FilterBox> <!-- filter로 반복문 돌리고 이 객체를 props전송 -->
      </div>
    </div>

    <!-- 글작성페이지 -->
    <div v-if="step == 2">
      <div class="upload-image" :style="`background-image:url(${image})`"></div>
      <div class="write">
        <textarea @input="$emit('write', $event.target.value)" class="write-box">write!</textarea>
      </div>
    </div>
  </div>
</template>

<script>
import Post from "./Post";
import FilterBox from "./FilterBox";
import filter from "../filter.js"

export default {
  name: "Container",
  components: {
    Post,
    FilterBox,
  },
  props: {
    postData: [Array, Object],
    step: Number,
    image: String,
  },
  data() {
    return {
      instagramFilter: filter,
    }
  },
};
</script>

<style>
.upload-image {
  width: 100%;
  height: 450px;
  background: cornflowerblue;
  background-size: cover;
}
.filters {
  overflow-x: scroll;
  white-space: nowrap;
}
.filter-1 {
  width: 100px;
  height: 100px;
  background-color: cornflowerblue;
  margin: 10px 10px 10px auto;
  padding: 8px;
  display: inline-block;
  color: white;
  background-size: cover;
}
.filters::-webkit-scrollbar {
  height: 5px;
}
.filters::-webkit-scrollbar-track {
  background: #f1f1f1;
}
.filters::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 5px;
}
.filters::-webkit-scrollbar-thumb:hover {
  background: #555;
}
.write-box {
  border: none;
  width: 90%;
  height: 100px;
  padding: 15px;
  margin: auto;
  display: block;
  outline: none;
}
</style>