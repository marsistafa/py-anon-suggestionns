<template>
  <div>
    <h2>Suggestions</h2>
    <ul>
      <li v-for="suggestion in suggestions" :key="suggestion.id">
        {{ suggestion.category }} - {{ suggestion.description }}
        <button @click="upvote(suggestion.id)">Upvote</button>
        <button @click="downvote(suggestion.id)">Downvote</button>
      </li>
    </ul>
</div>
<div>
    <h2>Add New Suggestion</h2>
    <form @submit.prevent="addSuggestion">
      <label>Category:</label>
      <input v-model="newSuggestion.category" required>
      <label>Description:</label>
      <input v-model="newSuggestion.description" required>
      <button type="submit">Add Suggestion</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      suggestions: ['here','fwaa'],
      newSuggestion: {
        category: '',
        description: '',
      },
    };
  },
  mounted() {
    this.fetchSuggestions();
  },
  methods: {
    async fetchSuggestions() {
      try {
        const response = await axios.get('http://127.0.0.1:8000/api/suggestions/');
        this.suggestions = response.data;
      } catch (error) {
        console.error('Error fetching suggestions:', error);
      }
    },
    async addSuggestion() {
      try {
        const response = await axios.post('http://127.0.0.1:8000/api/suggestions/', this.newSuggestion);
        this.suggestions.push(response.data);
        this.newSuggestion = { category: '', description: '' }; // Clear the form
      } catch (error) {
        console.error('Error adding suggestion:', error);
      }
    },
    async upvote(suggestionId) {
      try {
        await axios.post(`http://127.0.0.1:8000/api/suggestions/${suggestionId}/upvote/`);
        this.fetchSuggestions(); // Refresh the suggestions after voting
      } catch (error) {
        console.error('Error upvoting suggestion:', error);
      }
    },
    async downvote(suggestionId) {
      try {
        await axios.post(`http://127.0.0.1:8000/api/suggestions/${suggestionId}/downvote/`);
        this.fetchSuggestions(); // Refresh the suggestions after voting
      } catch (error) {
        console.error('Error downvoting suggestion:', error);
      }
    },
  },
};
</script>
