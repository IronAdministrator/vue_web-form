<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      terms: false,
      hours: [],
      tempSkill: "",
      skills: [],
      passwordError: '',
    };
  },
  methods: {
    addSkill(e) {
      // console.log(e);
      if (e.key === "," && this.tempSkill.length > 1) {
        if (!this.skills.includes(this.tempSkill.slice(0, -1))) {
          this.skills.push(this.tempSkill.slice(0, -1));
        }
        this.tempSkill = "";
      }
    },
    deleteSkill(skill) {
      // console.log(index);
      // this.skills.splice(index, 1) // this deletes and mutates the Index of Skill in the original array of skills
      // console.log(skill);
      this.skills = this.skills.filter((item) => {
        // this creates a new array and return it
        return skill !== item; // this returns everything where 'skill' is not equal to 'item'
      });
    },
    handleSubmit() {
      // console.log('Form Submitted!');
      this.passwordError = this.password.length > 5 ?
      '' : 'password must contain more than 5 characters!'

      if (!this.passwordError) {
        console.log(`email: ${this.email}`);
        console.log(`password: ${this.password}`);
        console.log(`role: ${this.role}`);
        console.log(`terms: ${this.terms}`);
        console.log(`hours: ${this.hours}`);
        console.log(`skills: ${this.skills}`);
      }
    }
  },
};
</script>

<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email" />

    <label>Password:</label>
    <input type="password" required v-model="password" />
    <div v-if="passwordError" class="error">{{passwordError}}</div>

    <label>Role:</label>
    <select v-model="role">
      <option value="developer">Web developer</option>
      <option value="designer">Web designer</option>
    </select>

    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup="addSkill" />
    <div v-for="(skill, index) in skills" :key="skill" class="pill">
      <!-- <span @click="deleteSkill(index)">{{skill}}</span> -->
      <span @click="deleteSkill(skill)">{{ skill }} <span style="color: lightcoral">✘</span></span>
    </div>

    <div class="terms">
      <input type="checkbox" required v-model="terms" />
      <label>Accept Terms and Conditions</label>
    </div>
    
    <label>Working Hours:</label>
    <div>
      <input type="checkbox" value="Full-time" v-model="hours" />
      <label>Full-time</label>
    </div>
    <div>
      <input type="checkbox" value="Part-time" v-model="hours" />
      <label>Part-time</label>
    </div>
    <div>
      <input type="checkbox" value="Basis" v-model="hours" />
      <label>Basis</label>
    </div>

    <div class="submit">
      <button>Create an Account</button>
    </div>
  </form>
</template>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}

label {
  color: #aaa;
  display: inline-block;
  /* margin: 25px 0 15px; */
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}

input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}

input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}
button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
    cursor: pointer;
  }
  .submit {
    text-align: center;
  }
  .error {
    color: lightcoral;
    font-size: 0.8em;
    font-weight: bold;
  }
</style>
