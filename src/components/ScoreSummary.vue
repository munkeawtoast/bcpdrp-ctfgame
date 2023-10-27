<script setup>
import { defineProps } from "vue";
const props = defineProps({
  scores: {
    type: Array,
    required: true,
  },
  questions: {
    type: Array,
    required: true,
  },
});

// <ScoreSummary :scores="choices" :questions="questions" />
</script>

<template>
  <div class="score-summary">
    <h2>Score Summary</h2>
    <div class="score-summary__scores">
      <div class="score-summary__score" v-for="score in scores">
        <div class="score-summary__score-choice">{{ score.choice }}</div>
        <div class="score-summary__score-impact">{{ score.impact }}</div>
      </div>
      <div class="score-summary__sum">
        <div class="score-summary__score-choice">Total</div>
        <div class="score-summary__score-impact">
          {{ scored }}
        </div>
      </div>
    </div>
    <h3 v-if="scored >= 150">
      คุณทำได้ดีมาก
      เท่านี้ก็มั่นใจได้ว่าบริษัทของคุณจะยังอยู่ได้แม้ว่าจะเจอกับอะไรก็ตาม
    </h3>
    <h3 v-else-if="scored >= 25 && scored < 150">
      ในฐานะประทานบริษัทของคุณนั้นถือว่ายังทำได้ดี
      แต่ก็ยังไม่ดีพอที่จะรองรับกับสถานการที่หลากหลาย ค่อยๆเรียนรู้ไปเรื่อยๆ
      เดี๋ยวก็ดีเอง
    </h3>
    <h3 v-else>
      บริษัทที่มีคุณเป็นหัวหน้าหรือผู้บริหารนั้นมีความเสี่ยงมาก
      ไปเรียนรู้มาใหม่นะ
    </h3>
  </div>
</template>

<script>
export default {
  data() {
    return {
      scored: this.scores.reduce((sum, score) => sum + score.impact, 0),
    };
  },
};
</script>
<style scoped>
.score-summary {
  margin: 2em 0;
}
.score-summary__scores {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 1em;

  align-items: stretch;
}
.score-summary__score {
  display: flex;
  justify-content: space-between;
  padding: 0.5em;
  border: 1px solid #646cff;
  border-radius: 0.5em;
}
.score-summary__score-choice {
  font-weight: bold;
  text-align: left;
}
.score-summary__score-impact {
  font-weight: bold;
}
.score-summary__sum {
  display: flex;
  justify-content: space-between;
  padding: 0.5em;
  border: 1px solid #646cff;
  border-radius: 0.5em;
  background-color: #646cff;
  color: white;
  grid-column: 1 / -1;
}
</style>
