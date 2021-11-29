<template>
  <div class="container">
    <h1>Form</h1>
    <form @submit.prevent="handleSubmit">
      <label>Email:</label>
      <input type="email" v-model="email" required>

      <label>Password:</label>
      <input type="password" v-model="password" required>
      <div v-if="passwordError" class="error">{{ passwordError }}</div>

      <label>Role:</label>
      <select v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
      </select>

      <label>Skills (press Comma to add):</label>
      <input type="text" v-model="tempSkill" @keyup.,="addSkill">
      <!-- <input type="text" v-model="tempSkill" @keyup.alt="addSkill"> -->
      <div v-for="skill in skills" :key="skill" class="pill">
        <span @click="deleteSkill(skill)">{{ skill }}</span>
      </div>

      <div class="terms">
        <input type="checkbox" v-model="terms" required>
        <label>Accept terms and conditions</label>
      </div>

      <div class="submit">
        <button class="btn btn--top-margin btn--display-block">Create an Account</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      role: 'developer',
      terms: false,
      skills: [],
      tempSkill: '',
      passwordError: null,
    }
  },
  methods: {
    addSkill($event) {
      if ($event.key === ',' && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill.slice(0, -1))
        }
        this.tempSkill = ''
      }
    },
    //
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item
      })
    },
    handleSubmit() {
      // validate password
      this.passwordError =
        this.password.length > 5
          ? ''
          : 'Password must be at least 6 characters long'

      if (!this.passwordError) {
        // make request to database to save user
        console.log('email: ', this.email)
        console.log('password: ', this.password)
        console.log('role: ', this.role)
        console.log('skills: ', this.skills)
        console.log('terms accepted: ', this.terms)
      }
    },
  },
}
</script>

