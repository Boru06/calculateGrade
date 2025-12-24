<template>
  <div>
    <v-card class="card" width="500px" height="300px">
      <v-card-title>Calculate Grade</v-card-title>
      <v-card-text>
        <v-text-field
          label="กรอกคะแนน (0 - 100)"
          v-model="score"
          type="number"
          outlined
        />

        <v-btn color="primary" block @click="calculateGrade"> คำนวณเกรด </v-btn>

        <v-alert v-if="error" type="error" class="mt-4" dense>
          {{ error }}
        </v-alert>

        <v-alert v-if="grade" type="success" class="mt-4" dense>
          เกรดที่ได้คือ: <strong>{{ grade }}</strong>
        </v-alert>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  name: "CalculateGrade",
  data() {
    return {
      score: "",
      grade: "",
      error: "",
      sum:0
    };
  },
  methods: {
    calculateGrade() {
      const scoreNum = parseFloat(this.score);
      // reset ค่าเดิมก่อน
      this.error = "";
      this.grade = "";

      if (isNaN(scoreNum) || scoreNum < 0 || scoreNum > 100) {
        this.error = "ตัวเลขที่ไม่อยู่ในช่วง 0 - 100 ";
        return;
      }
      if (scoreNum >= 90) {
        this.grade = "A";
      } else if (scoreNum >= 80) {
        this.grade = "B";
      } else if (scoreNum >= 70) {
        this.grade = "C";
      } else if (scoreNum >= 60) {
        this.grade = "D";
      } else {
        this.grade = "F";
      }
      setTimeout(() => {
        this.grade = "";
        this.error = "";
      }, 1000);
    },
  },
};
</script>

<style>
.card {
  margin: 50px auto;
  padding: 20px;
}
</style>