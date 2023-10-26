<template>
  <div class="radio-button">
    <div class="question">{{ question }}</div>
    <div class="choices">
      <label v-for="(choice, index) in choices" :key="choice" class="choice">
        <input
          type="radio"
          :name="question"
          :value="choice"
          v-model="selectedChoice"
        />
        <span>{{ choice.choice }}</span>
      </label>
    </div>
    <div class="submit-container">
      <button class="submit-button" @click="$emit('submit', selectedChoice)">
        {{ isLast ? "Submit" : "Next" }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "RadioButton",
  props: {
    index: {
      type: Number,
      required: true,
    },
    isLast: {
      type: Boolean,
      required: true,
    },
    question: {
      type: String,
      required: true,
    },
    choices: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      selectedChoice: null,
    };
  },
};
</script>

<style scoped>
.submit-container {
  display: flex;
  width: 100%;
  justify-content: flex-end;
  margin-top: 1rem;
}
.submit-button {
  margin-top: 1rem;
}
.radio-button {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-bottom: 1rem;
}

.question {
  font-size: 1.2rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
}

.choices {
  display: flex;
  flex-direction: column;
}

.choice {
  display: flex;
  align-items: center;
  margin-bottom: 0.5rem;
}

input[type="radio"] {
  margin-right: 0.5rem;
}
</style>
