<template>
  <form @submit.prevent="hSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email" />

    <label>Password:</label>
    <input type="password" required v-model="password" />
    <div v-if="passError" class="error">
      {{ passError }}
    </div>

    <label>Role:</label>
    <select v-model="role">
      <option value="developer">web developer</option>
      <option value="designer">web designer</option>
    </select>

    <!-- <div class="">
      <input type="checkbox" value="Ali" v-model="names">
      <label >Ali</label>
    </div>
    <div class="">
      <input type="checkbox" value="shaun" v-model="names">
      <label >shaun</label>
    </div>
    <div class="">
      <input type="checkbox" value="Omer" v-model="names">
      <label >Omer</label>
    </div> -->

    <label for="">Skills:</label>
    <input
      type="text"
      name=""
      id=""
      v-model="tempSkill"
      @keyup.alt="addSkill"
    />

    <div v-for="skill in skills" v-bind:key="skill" class="pill">
      <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>

    <div class="term">
      <input type="checkbox" required v-model="terms" />
      <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
      <button>Create an Account</button>
    </div>
  </form>
  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms accepted: {{ terms }}</p>
  <!-- <p>Names: {{ names }}</p> -->
  <p>Skills: {{ skills }}</p>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "developer",
      terms: false,
      tempSkill: "",
      skills: [],
      // names: [],
      passError: "",
    };
  },
  methods: {
    addSkill(e) {
      console.log(e);
      if (e.key === "," && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
          this.tempSkill = "";
        }
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item;
      });
    },
    hSubmit() {
      this.passError =
        this.password.length > 5 ? "" : "Passwod must be at least 6 chars long";

    },
  },
};
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
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
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
.error{
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
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
  padding: 10px 16px;
  margin-top: 20px;
  color: white;
  border-radius: 15px;
}
.submit {
  text-align: center;
}
</style>