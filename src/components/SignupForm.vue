<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <!-- v- model for two-way data binding -> data() email gets updated by the input field -->
    <input type="email" required v-model="email" />
    <label>Passwort:</label>
    <input type="password" required v-model="password" />
    <p style="color: rgb(236, 69, 69); font-weight: 700; margin-top: 10px" v-if="passwordError">
      {{ passwordError }}
    </p>

    <label>Rolle:</label>
    <select v-model="role" required>
      <option value="development">Web Entwicklung</option>
      <option value="design">Web Design</option>
      <option value="marketing">Marketing</option>
    </select>

    <label>Skills: (max. 8)</label>
    <p>z.B. HTML, CSS, JavaScript, Google SEO, usw...</p>
    <input type="text" v-model="tempSkill" @keyup="addSkill" />
    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="deleteSkill"> {{ skill }}</span>
    </div>

    <div class="terms">
      <input type="checkbox" v-model="terms" required />
      <label>Ich akzeptiere die Geschätsbedingungen.</label>
    </div>

    <div class="submit">
      <button>Create an Account</button>
    </div>

    <!-- <div>
      <input type="checkbox" value="shaun" v-model="names" />
      <label>Shaun</label>
    </div>
    <div>
      <input type="checkbox" value="peter" v-model="names" />
      <label>Peter</label>
    </div>
    <div>
      <input type="checkbox" value="frank" v-model="names" />
      <label>Frank</label>
    </div> -->
  </form>

  <p>Email: {{ email }}</p>
  <p>Passwort: {{ password }}</p>
  <p>{{ role }}</p>
  <p>{{ terms }}</p>
  <p>{{ names }}</p>
  <p>{{ skills }}</p>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      role: '',
      terms: false,
      names: [],
      tempSkill: '',
      skills: [],
      passwordError: ''
    }
  },
  methods: {
    addSkill(a) {
      if (a.key === ' ' && this.tempSkill && this.skills.length < 8) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill)
        }
        this.tempSkill = ''
      }
    },
    deleteSkill(a) {
      this.skills.splice(this.skills.indexOf(a.target.textContent), 1)
    },
    /*deleteSkillAlt(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item;
      })
    }*/
    handleSubmit(e) {
      //validate password
      /*if (this.password.length < 8) {
        alert('Passwort muss mindestens 8 Zeichen lang sein.')
        return
      }*/
      this.passwordError =
        this.password.length > 8 ? '' : 'Passwort muss mindestens 8 Zeichen lang sein'
      
      if (!this.passwordError) {
        e.preventDefault()
        console.log(this.email, this.password, this.role, this.terms, this.names, this.skills)
      }
    }
  }
}
</script>

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
  display: inline-blockck;
  margin: 25px 0 15px;
  color: #aaa;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}

p {
  display: inline-blockck;
  margin: 5px 0 15px;
  color: #b9b9b9;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}

input {
  display: block;
  width: 100%;
  padding: 10px 6px;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  margin: 0 0 20px;
  color: #b8b8b8;
}

input:focus {
  outline: none;
}

input[type='checkbox'] {
  display: inline-block;
  width: 20px;
  margin: 20 10px 0 0;
  position: relative;
  top: 2px;
}

select {
  width: 100%;
  padding: 10px 6px;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  margin: 0 0 20px;
  color: #474747;
}

option {
  font-size: 1.2em;
  padding: 10px;
  border: none;
  border-radius: 30px;
}

selet:focus {
  outline: none;
}

.pill {
  display: inline-block;
  margin: 20px 10px;
  padding: 10px 20px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}

button {
  background-color: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
}

button:hover {
  background-color: #0c61e2;
  cursor: pointer;
}

.submit {
  text-align: center;
}
</style>
