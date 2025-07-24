<template>
    <div>
        <form @submit.prevent="handleSubmit">
            <label>Email:</label>
            <input type="email" v-model="email" required>

            <label>Password:</label>
            <input type="password" v-model="password" required>
            <div v-if="passwordError" class="error">{{ passwordError }}</div>

            <label>Role:</label>
            <select v-model="role" required>
                <option value="developer">Web Developer</option>
                <option value="designer">Web Designer</option>
                <option value="datascientist">Data Scientist</option>
            </select>

            <label>Skills:</label>
            <input type="text" v-model="tempSkills" @keyup="addSkill">
            <div v-for="skill in skills" :key="skill" class="skill">
                <span @click="deleteSkills(skill)">{{ skill }}</span>
            </div>

            <div class="terms">
                <input type="checkbox" v-model="terms" required>
                <label>I agree to the terms and conditions</label>
            </div>

            <div class="submit">
            <button>Create Account</button>
            </div>
        </form>

        <p>Entered Email: {{ email }}</p>
        <p>Entered Password: {{ password }}</p>
        <p>Selected Role: {{ role }}</p>
        <p>Terms Accepted: {{ terms }}</p>

</div>
</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: '',
            terms: true,
            tempSkills: '',
            skills: [],
            passwordError: ''
        };
    },
    methods: {
        addSkill(event) {
            if (event.key === ',' && this.tempSkills) {
                event.preventDefault(); // 🛑 Prevent the comma from being inserted
                const skill = this.tempSkills.replace(',', '').trim();
                if (skill && !this.skills.includes(skill)) {
                    this.skills.push(skill)
                } 
                this.tempSkills = '';
            }
        },
        deleteSkills(skill) {
            this.skills = this.skills.filter((item) => {
                return skill !== item
            });
        },
        handleSubmit() {
            this.passwordError = this.password.length > 5 ? 
            '' : 'Password must be at least 5 characters long';
            if (!this.passwordError) {
                alert(`Account created for ${this.email} with role ${this.role}`);
                // Reset form
                this.email = '';
                this.password = '';
                this.role = '';
                this.terms = false;
                this.tempSkills = '';
                this.skills = [];
            }
        }
    }
}
</script>

<style>
form {
    max-width: 420px;
    margin: 30px auto;
    padding: 40px;
    background: white;
    border-radius: 10px;
    text-align: left;
}
label {
    display: inline-block;
    font-weight: bold;  
    color: #aaa;
    margin: 25px 0 15px;
    font-size: 0.9em;
    text-transform: uppercase;
    letter-spacing: 1px;
}

input, select {
    display: block;
    width: 100%;
    padding: 10px 6px;
    border: none;
    border-bottom: 1px solid #ddd;
    box-sizing: border-box;
    color: #555;    
}
input[type="checkbox"] {
    width: 16px;
    display: inline-block;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}
.skill {
    display: inline-block;
    background: #eee;
    padding: 6px 12px;
    margin: 20px 10px 0 0;
    border-radius: 20px;
    cursor: pointer;
    color: #777;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
}
button {
    background: #0b6dff;
    color: white;
    border: 0;
    border-radius: 20px;
    cursor: pointer;
    margin-top: 20px;
    width: auto;
    padding: 10px 20px;
    font-size: large;
}
.submit {
    text-align: center;
}
.error {
    color: red;
    font-size: 0.8em;
    margin-top: 5px;
    font-weight: bold;
}
</style>


<!--
Challenge -
1. when a user clicks on a skill, delete that skill from the list
-->