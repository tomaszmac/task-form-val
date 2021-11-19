<template>
  <form class="form" @submit.prevent="submitForm">
    <div class="form__field" :class="{ invalid: email.isNotValid }">
      <label for="email" class="form__label">Email</label>
      <input
        type="email"
        id="email"
        class="form__input"
        placeholder="e.g. email@email.com"
        v-model.trim="email.val"
        @blur="checkEmail('email')"
      />
    </div>
    <span class="form__val-message invalid">
      <p v-show="true">{{ email.message }}</p>
    </span>
    <div class="form__field" :class="{ invalid: password.isNotValid }">
      <label for="password" class="form__label">Password:</label>
      <input
        type="password"
        id="password"
        class="form__input"
        v-model.trim="password.val"
        @blur="checkPassword()"
      />
    </div>
    <span class="form__val-message invalid">
      <p v-show="password.isNotValid">{{ password.message }}</p>
    </span>
    <div class="form__field" :class="{ invalid: age.isNotValid }">
      <label for="age" class="form__label">Age</label>
      <input
        type="number"
        id="age"
        class="form__input"
        v-model.trim="age.val"
        @blur="checkAge()"
      />
    </div>
    <span class="form__val-message invalid">
      <p v-show="age.isNotValid">{{ age.message }}</p>
    </span>
    <button type="submit" class="btn form__button">Submit</button>
  </form>
</template>

<script>
import { ref, reactive } from "vue";

export default {
  name: "BaseForm",
  setup(_, { emit }) {
    const email = reactive({
      val: "",
      isNotValid: false,
      message: null,
    });

    const password = reactive({
      val: "",
      isNotValid: false,
      message: null,
    });

    const age = reactive({
      val: "",
      isNotValid: false,
      message: null,
    });

    const formIsValid = ref(false);

    function checkEmail() {
      const emReg = /\S+@\S+\.\S+/;
      const test = emReg.test(email.val);

      if (!test) {
        email.message = "Please provide correct email";
        email.isNotValid = true;
      } else {
        email.isNotValid = false;
        email.message = null;
      }
    }

    function checkPassword() {
      const isPasswordValid = password.val && password.val.length >= 8;

      if (!isPasswordValid) {
        password.message = "Password should be longer than 8 letters";
        password.isNotValid = true;
      } else {
        password.isNotValid = false;
      }
    }

    function checkAge() {
      const isAgeValid = age.val && +age.val > 18;

      if (!isAgeValid) {
        age.message = "Age should be at least 18";
        age.isNotValid = true;
      } else {
        age.isNotValid = false;
      }
    }

    function checkFields() {
      checkEmail();
      checkAge();
      checkPassword();

      if (email.isNotValid || password.isNotValid || age.isNotValid) {
        formIsValid.value = false;
      } else {
        formIsValid.value = true;
      }
    }

    function submitForm() {
      checkFields();

      if (formIsValid.value) {
        emit("submitForm", { email, password, age });
      }
    }

    return {
      email,
      password,
      age,
      checkEmail,
      checkPassword,
      checkAge,
      submitForm,
    };
  },
};
</script>

<style lang="scss" scoped>
.form {
  display: flex;
  flex-direction: column;
  padding: 0 2rem;

  @media (max-width: 480px) {
    padding: 0;
  }

  &__field {
    display: flex;
    justify-content: space-between;
    text-align: left;
    align-items: center;

    @media (max-width: 480px) {
      flex-direction: column;
      align-items: flex-start;
    }
  }

  &__label {
    font-size: 1.4rem;
    font-weight: 600;
    padding-bottom: 1rem;
  }

  &__input {
    box-sizing: border-box;
    flex: 0 0 66%;
    border-radius: 3px;
    padding: 1.6rem 1.2rem;
    margin-left: 2rem;
    margin-bottom: 0.4rem;
    border: 1px solid rgb(167, 167, 167);
    box-shadow: 0 2px 4px rgba(0, 44, 95, 0.2);

    &:focus {
      box-shadow: 0 0 0 0.15rem rgba(0, 44, 95, 0.6);
    }

    @media (max-width: 480px) {
      width: 100%;
      margin-left: 0;
    }
  }

  &__val-message {
    display: block;
    font-size: 1.2rem;
    text-align: right;
    height: 4rem;
    margin-top: -8px;
  }

  &__res-pass {
    justify-self: end;
  }

  &__link {
    display: block;
    text-decoration: none;
    color: var(--primary);
    font-size: 1.1rem;
    letter-spacing: 0.4px;
    font-weight: 600;
  }

  &__button {
    align-self: flex-end;
    outline: inherit;
    border: none;
    background-color: var(--primary);
    color: white;
    backface-visibility: hidden;
    transform: translateZ(0);
    box-shadow: 0 2px 4px rgba(0, 44, 95, 0.6);
    transition: all 0.2s;

    &:hover {
      transform: translateY(-1px);
      box-shadow: 0 4px 6px 1px rgba(0, 44, 95, 0.6);
    }

    &:active {
      transform: translateY(1px);
      box-shadow: 0 2px 2px rgba(0, 44, 95, 0.6);
    }
  }
}
</style>
