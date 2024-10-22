<template>
  <div>
    <h1>PR Disaster AI Game</h1>
    <p>Vote on actions for the AI to take!</p>
    <button @click="vote('attack')">Vote Attack</button>
    <button @click="vote('defend')">Vote Defend</button>
    
    <div v-if="decision">
      <h2>AI Decision</h2>
      <p>{{ decision }}</p>
    </div>

    <div>
      <h2>Current Votes</h2>
      <ul>
        <li>Attack: {{ votes.attack }}</li>
        <li>Defend: {{ votes.defend }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      votes: { attack: 0, defend: 0 },
      decision: null,
    };
  },
  methods: {
    vote(action) {
      this.$axios.post('http://localhost:3000/vote', { action })
        .then(response => {
          this.votes = response.data.votes;
          this.decision = response.data.decision;  // AI's decision after voting
        });
    }
  }
}
</script>
