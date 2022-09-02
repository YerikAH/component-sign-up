<script setup>
import { ref, watch } from "vue";
let firstName = ref("First Name");
let lastName = ref("Last Name");
let emailAddres = ref("Email Address");
let password = ref("Password");

let validationFirstName = ref(false);
let validationLastName = ref(false);
let validationEmailAddres = ref(false);
let validationPassword = ref(false);

let messageFirstName = ref("");
let messageLastName = ref("");
let messageEmailAddres = ref("");
let messagePassword = ref("");

let regexEmail = /^(\w+[/./-]?){1,}@[a-z]+[/.]\w{2,}$/;

let countMore = ref(1);
let countLast = ref(1);
let countEmail = ref(1);
let countPass = ref(1);
let typePass = ref("text");

let borderRedName = {
  border: "0.5px solid #6b6a6f85",
};
let borderRedLast = {
  border: "0.5px solid #6b6a6f85",
};
let borderRedEmail = {
  border: "0.5px solid #6b6a6f85",
  color: "#6b6a6f",
};
let borderRedPass = {
  border: "0.5px solid #6b6a6f85",
};

function handleBlur(e) {
  if (e.target.name == "first-name") {
    firstName.value = e.target.value;
    validation(firstName.value, e.target.name);
  } else if (e.target.name == "last-name") {
    lastName.value = e.target.value;
    validation(lastName.value, e.target.name);
  } else if (e.target.name == "email-addres") {
    emailAddres.value = e.target.value;
    validation(emailAddres.value, e.target.name);
  } else if (e.target.name == "password") {
    password.value = e.target.value;
    validation(password.value, e.target.name);
  }
}
function validation(input, name) {
  if (name == "first-name") {
    if (input == "") {
      validationFirstName.value = true;
      messageFirstName.value = "First Name cannot be empty";
    } else {
      validationFirstName.value = false;
    }
  } else if (name == "last-name") {
    if (input == "") {
      validationLastName.value = true;
      messageLastName.value = "Last Name cannot be empty";
    } else {
      validationLastName.value = false;
    }
  } else if (name == "email-addres") {
    if (input == "") {
      validationEmailAddres.value = true;
      messageEmailAddres.value = "Email cannot be empty";
    } else if (!regexEmail.test(input.trim())) {
      validationEmailAddres.value = true;
      messageEmailAddres.value = "Looks like this is not an email";
    } else {
      validationEmailAddres.value = false;
    }
  } else if (name == "password") {
    if (input == "") {
      validationPassword.value = true;
      messagePassword.value = "Password cannot be empty";
    } else {
      validationPassword.value = false;
    }
  }
}

function handleClick(e) {
  if (e.target.name == "first-name") {
    validationFirstName.value = false;
    if (countMore.value !== 2) {
      firstName.value = "";
      countMore.value = countMore.value + 1;
    }
  } else if (e.target.name == "last-name") {
    validationLastName.value = false;
    if (countLast.value !== 2) {
      lastName.value = "";
      countLast.value = countLast.value + 1;
    }
  } else if (e.target.name == "email-addres") {
    validationEmailAddres.value = false;
    if (countEmail.value !== 2) {
      emailAddres.value = "";
      countEmail.value = countEmail.value + 1;
    }
  } else if (e.target.name == "password") {
    validationPassword.value = false;
    if (countPass.value !== 2) {
      password.value = "";
      countPass.value = countPass.value + 1;
    }
  }
}

watch(validationFirstName, () => {
  if (validationFirstName.value == true) {
    borderRedName.border = "2px solid hsl(0, 100%, 74%)";
  } else if (validationFirstName.value == false) {
    borderRedName.border = "0.5px solid #6b6a6f85";
  }
});

watch(validationLastName, () => {
  if (validationLastName.value == true) {
    borderRedLast.border = "2px solid hsl(0, 100%, 74%)";
  } else if (validationLastName.value == false) {
    borderRedLast.border = "0.5px solid #6b6a6f85";
  }
});

watch(validationEmailAddres, () => {
  if (validationEmailAddres.value == true) {
    borderRedEmail.border = "2px solid hsl(0, 100%, 74%)";
    borderRedEmail.color = "hsl(0, 100%, 74%)";
  } else if (validationEmailAddres.value == false) {
    borderRedEmail.border = "0.5px solid #6b6a6f85";
    borderRedEmail.color = "#6b6a6f";
  }
});

watch(validationPassword, () => {
  if (validationPassword.value == true) {
    borderRedPass.border = "2px solid hsl(0, 100%, 74%)";
  } else if (validationPassword.value == false) {
    borderRedPass.border = "0.5px solid #6b6a6f85";
  }
});
watch(countPass, () => {
  typePass.value = "password";
});

function allClear() {
  firstName.value = "";
  lastName.value = "";
  emailAddres.value = "";
  password.value = "";
  validationFirstName.value = true;
  messageFirstName.value = "First Name cannot be empty";
  validationPassword.value = true;
  messagePassword.value = "Password cannot be empty";
  validationLastName.value = true;
  messageLastName.value = "Last Name cannot be empty";
  validationEmailAddres.value = true;
  messageEmailAddres.value = "Email cannot be empty";
}
function handleSubmit() {
  if (
    firstName.value == "First Name" ||
    lastName.value == "Last Name" ||
    emailAddres.value == "Email Address" ||
    password.value == "Password"
  ) {
    allClear();
  }
}
</script>

<template>
  <div class="found">
    <div class="img-found"></div>
  </div>
  <div class="grid-form_center">
    <div class="grid-form">
      <div class="grid-child_text">
        <h1>Learn to code by watching others</h1>
        <p>
          See how experienced developers solve problems in real-time. Watching
          scripted tutorials is great, but understanding how developers think is
          invaluable.
        </p>
      </div>
      <div class="grid-child_form">
        <div class="child_form-descount">
          <p><b>Try it free 7 days</b> then $20/mo. thereafter</p>
        </div>
        <div class="child_form_content">
          <form action="" class="child_form_content_form">
            <div class="container-inputs">
              <input
                name="first-name"
                type="text"
                class="content_form_input"
                @blur="handleBlur"
                :style="borderRedName"
                @click="handleClick"
                :value="firstName"
                required
              />
              <span v-show="validationFirstName" class="error-image"
                ><img src="../assets/icon-error.svg" alt="err"
              /></span>
            </div>
            <span v-show="validationFirstName" class="error-show">{{
              messageFirstName
            }}</span>

            <div class="container-inputs">
              <input
                name="last-name"
                type="text"
                class="content_form_input"
                @blur="handleBlur"
                @click="handleClick"
                :style="borderRedLast"
                :value="lastName"
                required
              />
              <span v-show="validationLastName" class="error-image"
                ><img src="../assets/icon-error.svg" alt="err"
              /></span>
            </div>
            <span v-show="validationLastName" class="error-show">{{
              messageLastName
            }}</span>
            <div class="container-inputs">
              <input
                name="email-addres"
                type="email"
                class="content_form_input"
                @blur="handleBlur"
                @click="handleClick"
                :style="borderRedEmail"
                :value="emailAddres"
                required
              />
              <span v-show="validationEmailAddres" class="error-image"
                ><img src="../assets/icon-error.svg" alt="err"
              /></span>
            </div>

            <span v-show="validationEmailAddres" class="error-show">{{
              messageEmailAddres
            }}</span>

            <div class="container-inputs">
              <input
                name="password"
                :type="typePass"
                class="content_form_input"
                @blur="handleBlur"
                @click="handleClick"
                :style="borderRedPass"
                :value="password"
                required
              />
              <span v-show="validationPassword" class="error-image"
                ><img src="../assets/icon-error.svg" alt="err"
              /></span>
            </div>
            <span v-show="validationPassword" class="error-show">{{
              messagePassword
            }}</span>
            <input type="submit" value="CLAIM YOUR FREE TRIAL" @click="handleSubmit" />
          </form>
          <p class="child_form_content_text">
            By clicking the button, you are agreeing to our
            <span>Terms and Services</span>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.found {
  background-color: var(--red);
  position: fixed;
  width: 100vw;
  height: 100vh;
}
.img-found {
  background-image: url("../assets/bg-intro-mobile.png");
  width: 100%;
  height: 100%;
  background-size: cover;
  background-attachment: fixed;
  background-position: center;
}
.grid-form_center {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}
@media (min-width: 500px) {
  .img-found {
    background-image: url("../assets/bg-intro-desktop.png");
  }
}
.grid-form {
  position: relative;
  max-width: 1110px;
}
@media (min-width: 1000px) {
  .grid-form {
    display: grid;
    grid-template-columns: 50% 50%;
    place-content: center;
    place-items: center;
    overflow: auto;
    width: 100%;
  }
}
.grid-child_text {
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 5rem 0 3rem 0;
}
.grid-child_text h1 {
  color: white;
  font-size: 2rem;
  max-width: 400px;
  line-height: 55px;
}
.grid-child_text p {
  color: white;
  margin: 1.29rem 0;
  line-height: 30px;
  padding: 0 1rem;
  max-width: 450px;
}
.child_form-descount {
  background: var(--blue);
  color: white;
  padding: 1rem 3rem;
  border-radius: 0.5em;
  text-align: center;
  width: 100%;
  line-height: 30px;
  box-shadow: 0px 7px 0px rgba(0, 0, 0, 0.15);
}
.child_form_content {
  margin-top: 2rem;
  background: white;
  border-radius: 0.5rem;
  display: grid;
  max-width: 450px;
  box-shadow: 0px 6px 0px rgba(0, 0, 0, 0.15);
}
.child_form_content {
  display: flex;
  width: 100%;
  padding: 2rem 1rem;
  flex-direction: column;
}
.content_form_input {
  padding: 1rem;
  border-radius: 0.5rem;
  width: 100%;
  border: 0.5px solid #6b6a6f85;
  font-size: 0.85rem;
  font-weight: 600;
  outline: none;
  margin-bottom: 1rem;
  color: #6b6a6f;
}
.content_form_input:focus {
  color: var(--dark-blue);
  border: 1px solid var(--dark-blue) !important;
}
.content_form_input::placeholder {
  color: #6b6a6f;
  opacity: 1;
}
.child_form_content input[type="submit"] {
  padding: 1rem;
  border: none;
  border-radius: 0.5rem;
  background-color: var(--green);
  color: white;
  font-size: 1rem;
  font-weight: 700;
  width: 100%;
  letter-spacing: 0.1em;
  font-size: 0.85rem;
  box-shadow: inset 0px -5px 0px rgba(0, 0, 0, 0.1);
  transition: 0.3s;
  cursor: pointer;
}
.child_form_content input[type="submit"]:hover {
  background-color: #77e2b4;
}
.grid-child_form {
  padding: 0 1rem;
  display: flex;
  width: 100%;
  align-items: center;
  flex-direction: column;
  margin-bottom: 6rem;
}
@media (min-width: 1000px) {
  .grid-child_form {
    margin: 0;
    height: 100%;
  }
  .grid-child_text {
    width: 100%;
    height: 100%;
    padding: 0;
  }
}
@media (min-width: 1000px) {
  .grid-child_form,
  .grid-child_text {
    justify-content: center;
  }
}
.child_form_content_form {
  width: 100%;
  display: flex;
  align-items: center;
  flex-direction: column;
}
.child_form_content_text {
  text-align: center;
  color: #b9b8c0;
  margin-top: 1rem;
  font-size: 0.8rem;
  padding: 0 1rem;
}
.child_form_content_text span {
  font-weight: 600;
  color: var(--red);
}
@media (min-width: 1000px) {
  .content_form_input {
    margin-bottom: 1.5rem;
    font-size: 1rem;
    padding: 1rem 2rem;
  }
  .child_form_content {
    max-width: none;
  }
  .child_form_content input[type="submit"] {
    letter-spacing: 0;
    font-size: 1rem;
    font-weight: 600;
  }
  .grid-child_text h1 {
    font-size: 2.97rem;
    max-width: none;
    text-align: left;
  }
  .grid-child_text p {
    max-width: none;
    padding: 0;
    text-align: left;
  }
  .grid-child_text {
    padding: 0 1rem;
  }
  .child_form_content {
    padding: 2rem;
  }
  .child_form_content_text {
    font-size: 0.67rem;
  }
}
@media (min-height: 610px) {
  .grid-form {
    grid-template-rows: 100vh;
    height: 100vh;
  }
}
.error-show {
  width: 100%;
  text-align: right;
  font-size: 0.7rem;
  font-style: italic;
  position: relative;
  top: -13px;
  padding: 0 0.5rem 0 0;
  color: var(--red);
  font-weight: 500;
}
.container-inputs {
  width: 100%;
  position: relative;
}
.error-image {
  position: absolute;
  top: 0;
  right: 0;
  margin: 1rem;
}
</style>
