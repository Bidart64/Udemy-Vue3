<template>
  <section>
    <base-card>
      <h2>Submitted Experiences</h2>
      <div>
        <base-button @click="loadExperiences">Load Submitted Experiences</base-button>
      </div>
      <!-- <p v-if="isLoading">Loading</p> -->
      <!-- <p v-else-if="!results?.length > 0">No stored experiences found. Start adding some surveys results.</p> -->
      <!-- <p v-else-if="error">{{ error }}</p> -->
      <!-- <ul v-else> -->
      <ul>
        <survey-result
          v-for="result in results"
          :key="result.id"
          :name="result.name"
          :rating="result.rating"
        ></survey-result>
      </ul>
    </base-card>
  </section>
</template>

<script>
import SurveyResult from './SurveyResult.vue';
import axios from 'axios';
import config from '../../config.js';
export default {
  components: {
    SurveyResult,
  },
  data() {
    return {
      results: [],
      isLoading: false,
      error: null,
    };
  },
  methods: {
    async loadExperiences() {
      try {
        this.isLoading = true;
        this.error = null;
        const response = await axios.get(config.firebaseURL);
        this.results = Object.entries(response.data).map(([key, value]) => {
          return {
            id: key,
            ...value
            }
          });
        this.isLoading = false;
        return 
      } catch (error) {
        this.error = 'Failed to fetch data - please try again later.';
      }
    },
  },
  mounted() {
    this.loadExperiences();
  } 
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>