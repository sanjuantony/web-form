<template>
    <form @submit.prevent="submitData">
        <label>Email Id: </label>
        <input type="email" required v-model="_email" />
        <br>
        <label>Password: </label>
        <input type="password" required v-model="_password" />
        <div v-if="_passwordError"> {{ this._passwordError }}</div>
        <br>
        <label>Role: </label>
        <select v-model="_role">
            <option value="web_developer">Web Developer</option>
            <option value="web_designer">Web Designer</option>
        </select>
        <br>
        <label>Accept T&C: </label>
        <input type="checkbox" v-model="_terms" />
        <br>
        <label>Skills: </label>
        <input type="text" v-model="_tempSkill" @keyup.alt="addSkill" />

        <div class="submit">
            <button>Create and Account</button>
        </div>
    </form>

    <p>Email Id: {{ _email }}, Password: {{ _password }}, Role: {{ _role }}, Accepted T&C: {{ _terms }}</p>
    <!-- <p>Names: {{ _names }}</p> -->
    <div>
        <label v-for="skill in _skills" :key="skill" @click="deleteSkill(skill)" class="pill">
            {{ skill }}
        </label>
    </div>
    
</template>

<script>
export default {
    data() {
        return {
            _email: "",
            _password: "",
            _role: "",
            _terms: false,
            _tempSkill: "",
            _skills: [],
            _passwordError: ""
            // _names: []
        }
    }, 
    methods: {
        addSkill(e) {
            console.log (e)
            if( e.key === "," && this._tempSkill ) {
                this._skills.push(this._tempSkill)
                this._tempSkill = ""
            }
        },
        deleteSkill(skill) {
            console.log(skill)
            var _index = this._skills.indexOf(skill)
            this._skills.splice(_index,1)
        },
        submitData() {
            this._passwordError = this._password.length > 5 ? "" : "Password needs to be atleat 6 chars long" 
            console.log("Email ID: "+this._email+", Password: "+this._password+", Role: "+this._role)
            console.log("T&C Accepted: "+this._terms+", Skills: "+this._skills)
        }
    }
}
</script>

<style>
    form {
        background-color: whitesmoke;
        border-radius: 20px;
        max-width: 400px;
        height: 400px;
        margin: 20px auto;
        text-align: left;
    }
    label {
        color: rgb(129, 114, 111);
        font-style: bold;
        margin-left: 10px;
    }
    label.pill {
        display: inline-block;
        margin: 20px 10px 0px 0px;
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
        border-radius: 20px;
        background: blue;
        color: white;
        padding: 10px 20px;
        border: 0px;
        margin-top: 20px;
    }
    div.submit {
        text-align: center;
    }
</style>