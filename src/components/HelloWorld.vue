<template>
  <v-card class="card" max-width="440" elevation="2">
    <div>
      <h1 class = "title-text">กรอกคะแนน</h1>
      <p class="subtitle-text">กรอกคะแนนแล้วกดปุ่มเพื่อดูเกรดที่ได้</p>
  

      <v-text-field 
        name="score" 
        label="กรอกคะแนน(0-100)" 
        id = "score" 
        v-model="score"
        prepend-inner-icon="mdi-pencil-outline"
        @keyup.enter="checkGrade()"
      >
      </v-text-field>

      <v-btn color="primary" @click="checkGrade()">ตัดเกรด</v-btn>

      <v-alert
          v-if="error"
          type="error"
          variant="tonal"
          density="compact"
          class="mt-4"
        >
          {{ error }}
        </v-alert>

      <div v-if="grade" class="result-box">
          <span class="grade-letter" :style="{ color: gradeColor }">
            {{ grade }}
          </span>
          <span class="result-text">
            คะแนน <strong>{{ value }}</strong> คะแนน
          </span>
        </div>

        <table class="range-table">
          <tr v-for="g in ranges" :key="g.letter" :class="{ active: grade === g.letter }">
            <td>{{ g.letter }}</td>
            <td>{{ g.min }} - {{ g.max }}</td>
          </tr>
        </table>
    </div>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      score: '',
      value: null,
      grade: '',
      error: '',
      ranges: [
        { letter: 'A', min: 80, max: 100, color: '#2E7D5B' },
        { letter: 'B', min: 70, max: 79,  color: '#3D5A80' },
        { letter: 'C', min: 60, max: 69,  color: '#B08900' },
        { letter: 'D', min: 50, max: 59,  color: '#C2622C' },
        { letter: 'F', min: 0,  max: 49,  color: '#B3392F' }
      ]
    }
  },

  computed: {
    gradeColor() {
      const found = this.ranges.find(g => g.letter === this.grade);
      return found ? found.color : '#000000';
    }
  },

  methods: {
    checkGrade(){
      this.grade = '';
      this.value = null;
      this.error = '';

      const raw = this.score.trim();

      if (raw === '') {
        this.error = 'กรุณากรอกคะแนนก่อน Enter';
        return;
      }

      const num = Number(raw);

       if (isNaN(num)) {
        this.error = 'กรุณากรอกเป็นตัวเลขเท่านั้น ห้ามกรอกตัวอักษร';
        return;
      }

      if (num < 0 || num > 100) {
        this.error = 'คะแนนต้องอยู่ในช่วง 0 - 100 เท่านั้น';
        return;
      }

      this.value = num;

      
      if (num >= 80) {
        this.grade = 'A';
      } else if (num >= 70) {
        this.grade = 'B';
      } else if (num >= 60) {
        this.grade = 'C';
      } else if (num >= 50) {
        this.grade = 'D';
      } else {
        this.grade = 'F';
      }
    }
  }
}
</script>

<style>

  .card {
    width: 100%;
    padding: 28px;
    border-radius: 8px;
  }

  .title-text {
    margin: 0 0 4px;
    font-size: 22px;
    color: #32B531;
  }

  .subtitle-text {
    margin: 0 0 20px;
    font-size: 14px;
    color: #6B7A87;
  }

  .result-box {
    display: flex;
    align-items: baseline;
    gap: 16px;
    margin-top: 24px;
    padding-top: 20px;
    border-top: 1px solid #E0E0E0;
  }

  .grade-letter {
  font-size: 72px;
  line-height: 0.85;
  font-weight: 500;
}

.result-text {
  font-size: 15px;
  color: #6B7A87;
}

.range-table {
  width: 100%;
  margin-top: 24px;
  border-collapse: collapse;
  font-size: 13px;
  color: #90A4AE;
}

.range-table td {
  padding: 6px 0;
  border-top: 1px solid #ECEFF1;
}

.range-table td:last-child {
  text-align: right;
}

.range-table tr.active td {
  color: #22303C;
  font-weight: 700;
}
</style>
