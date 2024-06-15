<template>
  <div class="titleProject">
    <h1>Aplikacija za validaciju lozinke</h1>
    <h3>
      Unesite željenu lozinku i pritisnite gumb <br />Provjerite ispunjava li vaša lozinka
      kriterije jake lozinke za bolju sigurnost.
    </h3>
  </div>
  <div v-if="showButtonMessage">
    <p class="message">
      Savjet: Lozinka treba imati minimalno 8 znakova, <br />
      koristiti kombinaciju malih i velikih slova i posebnih znakova!
    </p>
  </div>

  <form @submit.prevent="comparePassword">
    <div class="input__Password">
      <input v-model="inputPassword" id="inputString" type="text" required />
      <button type="submit">Provjeri</button>
    </div>
    <div v-if="check" style="text-align: center">
      <p class="message">
        Vaša lozinka nam je jakoooo poznata, nalazi se u popisu često korištenih lozinki!
      </p>
      <img
        class="image__WrongOrCheckmark"
        src="../public/resources/images/jack-sparrow-pirates.gif"
      />
    </div>
    <div v-else-if="comparisonResult !== null">
      <div v-if="comparisonResult" style="text-align: center">
        <p class="message">Vaša lozinka zadovoljava standarde sigurnosti!</p>
        <img
          class="image__WrongOrCheckmark"
          src="../public/resources/images/checkmark.svg"
        />
      </div>
      <div v-else style="text-align: center">
        <p class="message">
          Vaša lozinka može biti bolja. <br />Ovakva lozinka ne zadovoljava standarde
          sigurnosti.
        </p>
        <img class="image__WrongOrCheckmark" src="../public/resources/images/wrong.svg" />
      </div>
    </div>
  </form>
  <div class="buttonDiv">
    <button @click="showMessage">Savjet</button>
  </div>

  <Footer />
</template>

<script setup>
import { ref } from "vue";
const showMessage = () => {
  showButtonMessage.value = !showButtonMessage.value;
};

const showButtonMessage = ref(false);

const inputPassword = ref("");
const comparisonResult = ref(null);
const check = ref(null);
const passwordsToCompare = [
  "123456",
  "123456789",
  "qwerty",
  "password",
  "12345",
  "12345678",
  "123123",
  "111111",
  "1234",
  "1234567",
  "1234567890",
  "qwertyuiop",
  "1q2w3e4r5t",
  "000000",
  "abc123",
  "654321",
  "123",
  "1qaz2wsx",
  "admin",
  "letmein",
  "monkey",
  "666666",
  "7777777",
  "123qwe",
  "qwe123",
  "qwerty123",
  "1q2w3e",
  "iloveyou",
  "zxcvbnm",
  "asdfghjkl",
  "123abc",
  "987654321",
  "password1",
  "888888",
  "112233",
  "1qazxsw2",
  "qazwsx",
  "123321",
  "1qaz2wsx3edc",
  "a123456",
  "121212",
  "dragon",
  "welcome",
  "football",
  "soccer",
  "1qaz2wsx3edc4rfv",
  "baseball",
  "abcdef",
  "aaaaaa",
  "666666",
  "password123",
  "123654",
  "mypassword",
  "letmein123",
  "qweasdzxc",
  "qazwsxedc",
  "trustno1",
  "sunshine",
  "superman",
  "iloveyou2",
  "0987654321",
  "qazxsw",
  "hello",
  "master",
  "password!",
  "princess",
  "159753",
  "michael",
  "777777",
  "987654",
  "q1w2e3r4",
  "love",
  "123123123",
  "admin123",
  "admin1",
  "p@ssw0rd",
  "letmein!",
  "secret",
  "welcome123",
  "qazxswedc",
  "test",
  "root",
  "!@#$%^&*",
  "adminadmin",
  "1q2w3e4r",
  "q1w2e3",
  "monkey123",
  "dragon123",
  "1q2w3e4r5",
  "test123",
  "qaz123",
  "qwerty1",
  "qazwsxedcrfv",
  "zxcvbn",
  "asdf1234",
  "zxc123",
  "qazxsw123",
  "a1b2c3",
  "test1",
  "asdfgh",
];

const comparePassword = () => {
  const hasUpperCase = /[A-Z]/.test(inputPassword.value);
  const hasLowerCase = /[a-z]/.test(inputPassword.value);
  const hasSpecialChar = /[!@#$%^&*(),.?":{}|<>]/.test(inputPassword.value);
  const moreThanEightLChar = inputPassword.value.length > 7;

  const isValidPassword =
    hasUpperCase && hasLowerCase && hasSpecialChar && moreThanEightLChar;
  const isPasswordInList = passwordsToCompare.includes(inputPassword.value);

  check.value = isPasswordInList;

  comparisonResult.value = isValidPassword && !isPasswordInList;
};
</script>
