<script setup>
import { ref } from "vue";
import HelloWorld from "./components/HelloWorld.vue";
import Question from "./components/Question.vue";
import ScoreSummary from "./components/ScoreSummary.vue";

const questions = [
  {
    description:
      "คุณสังเกตเห็นว่าปริมาณการเข้าชมเว็บไซต์ลดลงอย่างรวดเร็ว การกระทำแรกของคุณคืออะไร",
    choices: [
      {
        choice: "วิเคราะห์ปริมาณการเข้าชมและตรวจสอบปัญหาของเซิร์ฟเวอร์",
        impact: 20,
      },
      {
        choice: "ละเว้นไว้ก่อน อาจเป็นความผันผวนชั่วคราว",
        impact: -10,
      },
      {
        choice: "โทรหาทีมการตลาดเพื่อสอบสวนปัญหา",
        impact: -5,
      },
    ],
  },
  {
    description: "ระบบซอฟต์แวร์ที่สำคัญล่มสลาย การตอบสนองของคุณโดยทันทีคือ?",
    choices: [
      {
        choice: "เรียกใช้แผนการกู้คืนจากภัยพิบัติและเปลี่ยนไปใช้ระบบสำรอง",
        impact: 25,
      },
      {
        choice: "พยายามรีสตาร์ทซอฟต์แวร์โดยไม่ต้องตรวจสอบเพิ่มเติม",
        impact: -30,
      },
      {
        choice: "แจ้งให้ทีมหยุดงานและจัดการในวันพรุ่งนี้",
        impact: -15,
      },
    ],
  },
  {
    description:
      "คุณได้รับอีเมลนิรนามแจ้งเตือนเกี่ยวกับการละเมิดความปลอดภัยที่อาจเกิดขึ้น คุณจะทำอย่างไร",
    choices: [
      {
        choice: "รายงานอีเมลไปยังทีมความปลอดภัยด้านไอทีทันที",
        impact: 20,
      },
      {
        choice: "เมินเฉย อาจเป็นเรื่องหลอกลวง",
        impact: -20,
      },
      {
        choice: "ส่งต่ออีเมลไปให้เพื่อนร่วมงานเพื่อขอคำแนะนำ",
        impact: -10,
      },
    ],
  },
  {
    description:
      "เกิดไฟไหม้ที่สำนักงานกลางของคุณ คุณและทีมงานของคุณจะดำเนินการอย่างไร",
    choices: [
      {
        choice: "อพยพออกจากอาคารทันทีและโทรเรียกรถดับเพลิง",
        impact: 25,
      },
      {
        choice: "พยายามดับไฟด้วยตนเองเพื่อประหยัดเวลา",
        impact: -30,
      },
      {
        choice: "รอคำสั่งจากผู้จัดการก่อนดำเนินการใดๆ",
        impact: -15,
      },
    ],
  },
  {
    description:
      "เกิดภัยพิบัติทางธรรมชาติ เช่น พายุหรือแผ่นดินไหวในพื้นที่ของคุณ บริษัทของคุณจะรับมืออย่างไร",
    choices: [
      {
        choice:
          "เปิดใช้งานแผน BCP และโยกย้ายพนักงานและอุปกรณ์ไปยังสถานที่ปลอดภัย",
        impact: 25,
      },
      {
        choice: "ให้พนักงานทำงานจากที่บ้านจนกว่าสถานการณ์จะกลับสู่ภาวะปกติ",
        impact: 20,
      },
      {
        choice: "ปิดบริษัทจนกว่าจะประเมินความเสียหายและทำการซ่อมแซมเสร็จสิ้น",
        impact: -15,
      },
    ],
  },
  {
    description:
      "เกิดการโจมตีทางไซเบอร์ต่อบริษัทของคุณ บริษัทของคุณจะรับมืออย่างไร",
    choices: [
      {
        choice:
          "รายงานการโจมตีไปยังทีมความปลอดภัยด้านไอทีทันทีและแยกเครือข่ายออกจากอินเทอร์เน็ต",
        impact: 25,
      },
      {
        choice: "พยายามแก้ไขด้วยตนเอง",
        impact: -30,
      },
      {
        choice: "รอให้ทีมความปลอดภัยด้านไอทีแก้ไขปัญหาก่อนดำเนินการใดๆ",
        impact: -15,
      },
    ],
  },
  {
    description:
      "พนักงานของคุณคนหนึ่งถูกขโมยข้อมูลสำคัญของบริษัท คุณจะทำอย่างไร",
    choices: [
      {
        choice:
          "รายงานการโจรกรรมข้อมูลไปยังทีมความปลอดภัยด้านไอทีทันทีและแจ้งให้พนักงานคนอื่นๆ ทราบ",
        impact: 25,
      },
      {
        choice: "พยายามติดต่อพนักงานคนนั้นเพื่อขอข้อมูลคืน",
        impact: -30,
      },
      {
        choice: "รอให้ทีมความปลอดภัยด้านไอทีสืบสวนก่อนดำเนินการใดๆ",
        impact: -15,
      },
    ],
  },
  {
    description:
      "ระบบจ่ายไฟฟ้าหลักขัดข้อง ทำให้สำนักงานของคุณไม่มีไฟฟ้าใช้ คุณจะทำอย่างไร",
    choices: [
      {
        choice: "เปิดใช้งานแผน BCP และเปลี่ยนไปใช้เครื่องผลิตไฟฟ้าสำรอง",
        impact: 25,
      },
      {
        choice:
          "แจ้งให้พนักงานหยุดงานและทำงานจากที่บ้านจนกว่าไฟฟ้าจะกลับมาใช้ได้ตามปกติ",
        impact: 10,
      },
      {
        choice: "ปิดสำนักงานจนกว่าไฟฟ้าจะกลับมาใช้ได้ตามปกติ",
        impact: -20,
      },
    ],
  },
  {
    description:
      "เกิดการประท้วงใหญ่ในพื้นที่ของคุณ ทำให้พนักงานไม่สามารถเดินทางได้ คุณจะทำอย่างไร",
    choices: [
      {
        choice: "เปิดใช้งานแผน BCP และให้พนักงานทำงานจากที่บ้าน",
        impact: 20,
      },
      {
        choice: "แจ้งให้พนักงานหยุดงานและรอให้สถานการณ์สงบลงก่อน",
        impact: -15,
      },
      {
        choice: "จัดหารถรับส่งพนักงานไปยังสถานที่ทำงาน",
        impact: -10,
      },
    ],
  },
  {
    description:
      "เกิดภัยพิบัติทางสังคม เช่น การระบาดของโรคระบาดหรือสงครามในพื้นที่ของคุณ บริษัทของคุณจะรับมืออย่างไร",
    choices: [
      {
        choice: "เปิดใช้งานแผน BCP และอนุญาตให้พนักงานทำงานจากที่บ้าน",
        impact: 25,
      },
      {
        choice: "ปิดสำนักงานและจัดหาเงินช่วยเหลือพนักงาน",
        impact: -15,
      },
      {
        choice: "ย้ายสำนักงานไปยังสถานที่ปลอดภัย",
        impact: 10,
      },
    ],
  },
];

let currentIndex = ref(0);
let choices = ref([
  // {
  //   choice: "Conduct a traffic analysis and check for server issues",
  //   impact: 20,
  // },
  // {
  //   choice: "Invoke the disaster recovery plan and switch to a backup system",
  //   impact: 25,
  // },
  // {
  //   choice: "Immediately report the email to the IT security team",
  //   impact: 20,
  // },
]);

function handleQuestionSubmit(choice) {
  choices.value.push(choice);
  currentIndex.value++;
}
</script>

<template>
  <div class="question-index">
    <!-- <img
      class="logo"
      src="./assets/logo.png"
      alt="logo"
      @mouseover="$event.target.src = './assets/logo-vue.png'"
      @mouseout="$event.target.src = './assets/logo.png'"
    /> -->
    <h1>Business Continuity Plan & Disaster Recovery Plan</h1>
    <h3 v-if="currentIndex !== questions.length">
      Question {{ currentIndex + 1 }} of ?
    </h3>
  </div>
  <Question
    v-for="(question, index) in questions"
    v-show="currentIndex === index"
    @submit="handleQuestionSubmit"
    :index="index"
    :is-last="index === questions.length - 1"
    :question="question.description"
    :choices="question.choices"
  />
  <ScoreSummary
    v-if="currentIndex === questions.length"
    :scores="choices"
    :questions="questions"
  />
  <div v-if="currentIndex === questions.length">
    <h3 v-if="choices >= 150">
      คุณทำได้ดีมาก
      เท่านี้ก็มั่นใจได้ว่าบริษัทของคุณจะยังอยู่ได้แม้ว่าจะเจอกับอะไรก็ตาม
    </h3>
    <h3 v-else-if="choices < 150 && choices >= 25">
      ในถานะประทานบริษัทของคุณนั้นถือว่ายังทำได้ดี
      แต่ยังไม่ดีพอที่จะรองรับกับสถานการที่หลากหลาย ค่อยๆเรียนรู้ไปเรื่อยๆ
      เดี๋ยวก็ดีเอง
    </h3>
    <h3 v-else>
      บริษัทที่มีคุณเป็นหัวหน้าหรือผู้บริหารนั้นมีความเสี่ยงมาก
      ไปเรียนรู้มาใหม่นะ
    </h3>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
