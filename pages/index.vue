<template>
  <div>
    <div class="titleProject">
      <h1>Aplikacija za validaciju lozinke</h1>
      <h3>
        Unesite željenu lozinku i pritisnite gumb <br />
        Provjerite ispunjava li vaša lozinka kriterije jake lozinke za bolju sigurnost.
      </h3>
    </div>
    <div v-if="showButtonMessage">
      <p class="message">
        Savjet: Lozinka treba imati minimalno 12 znakova, <br />
        koristiti kombinaciju malih i velikih slova i posebnih znakova!
      </p>
    </div>

    <form @submit.prevent="comparePassword">
      <div class="input__Password">
        <input v-model="inputPassword" id="inputString" type="text" required />
        <div class="form__ButtonDiv">
          <button type="submit" @click="handleHashing()">Provjeri Lozinku</button>
          <button @click="showHashMessage">Hashirana Lozinka</button>
        </div>
      </div>
      <div v-if="check" style="text-align: center">
        <p class="message">
          Vaša lozinka nam je jakoooo poznata, nalazi se u popisu često korištenih
          lozinki!
        </p>
        <img
          class="image__WrongOrCheckmark"
          src="../public/resources/images/jack-sparrow-pirates.gif"
        />
      </div>
      <div v-else-if="comparisonResult !== null">
        <div v-if="comparisonResult" style="text-align: center">
          <p class="message">Vaša lozinka zadovoljava standarde sigurnosti!</p>
          <p class="message" v-if="showHash">
            Kada bi koristili neki od načina kriptiranja kao npr. Hashiranje u bazi
            podataka bi vaša lozinka izgledala ovako:<br></br> {{ encryptedPassword }} <br />
            S time dodatno štitite lozinku jer ako netko i probije Vaš sustav i ukrade
            hashiranu lozinku, jako će teško doći do originala.
          </p>
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
          <img
            class="image__WrongOrCheckmark"
            src="../public/resources/images/wrong.svg"
          />
        </div>
      </div>
    </form>
    <div class="buttonDiv">
      <button @click="showMessage">Savjet</button>
    </div>

    <Footer />
  </div>
</template>

<script setup>
import { ref } from "vue";

const showMessage = () => {
  showButtonMessage.value = !showButtonMessage.value;
};

const showHashMessage = () => {
  showHash.value = !showHash.value;
};
const showHash = ref(null);
const showButtonMessage = ref(false);
const inputPassword = ref("");
const comparisonResult = ref(null);
const check = ref(null);
const encryptedPassword = ref("");
const passwordsToCompare = [
  "12345",
  "123456",
  "123456789",
  "test1",
  "password",
  "12345678",
  "zinch",
  "g_czechout",
  "asdf",
  "qwerty",
  "1234567890",
  "1234567",
  "Aa123456.",
  "iloveyou",
  "1234",
  "abc123",
  "111111",
  "123123",
  "dubsmash",
  "test",
  "princess",
  "qwertyuiop",
  "sunshine",
  "BvtTest123",
  "11111",
  "ashley",
  "00000",
  "000000",
  "password1",
  "monkey",
  "livetest",
  "55555",
  "soccer",
  "charlie",
  "asdfghjkl",
  "654321",
  "family",
  "michael",
  "123321",
  "football",
  "baseball",
  "q1w2e3r4t5y6",
  "nicole",
  "jessica",
  "purple",
  "shadow",
  "hannah",
  "chocolate",
  "michelle",
  "daniel",
  "maggie",
  "qwerty123",
  "hello",
  "112233",
  "jordan",
  "tigger",
  "666666",
  "987654321",
  "superman",
  "12345678910",
  "summer",
  "1q2w3e4r5t",
  "fitness",
  "bailey",
  "zxcvbnm",
  "fuckyou",
  "121212",
  "buster",
  "butterfly",
  "dragon",
  "jennifer",
  "amanda",
  "justin",
  "cookie",
  "basketball",
  "shopping",
  "pepper",
  "joshua",
  "hunter",
  "ginger",
  "matthew",
  "abcd1234",
  "taylor",
  "samantha",
  "whatever",
  "andrew",
  "1qaz2wsx3edc",
  "thomas",
  "jasmine",
  "animoto",
  "madison",
  "987654321",
  "54321",
  "flower",
  "Password",
  "maria",
  "babygirl",
  "lovely",
  "sophie",
  "Chegg123",
  "computer",
  "qwe123",
  "anthony",
  "1q2w3e4r",
  "peanut",
  "bubbles",
  "asdasd",
  "qwert",
  "1qaz2wsx",
  "pakistan",
  "123qwe",
  "liverpool",
  "elizabeth",
  "harley",
  "chelsea",
  "familia",
  "yellow",
  "william",
  "george",
  "7777777",
  "loveme",
  "123abc",
  "letmein",
  "oliver",
  "batman",
  "cheese",
  "banana",
  "testing",
  "secret",
  "angel",
  "friends",
  "jackson",
  "aaaaaa",
  "softball",
  "chicken",
  "lauren",
  "andrea",
  "welcome",
  "asdfgh",
  "robert",
  "orange",
  "Testing1",
  "pokemon",
  "555555",
  "melissa",
  "morgan",
  "123123123",
  "qazwsx",
  "diamond",
  "brandon",
  "jesus",
  "mickey",
  "olivia",
  "changeme",
  "danielle",
  "victoria",
  "gabriel",
  "123456a",
  "0.00000000",
  "loveyou",
  "hockey",
  "freedom",
  "azerty",
  "snoopy",
  "skinny",
  "myheritage",
  "qwerty1",
  "159753",
  "forever",
  "iloveu",
  "killer",
  "joseph",
  "master",
  "mustang",
  "hellokitty",
  "school",
  "Password1",
  "patrick",
  "blink182",
  "tinkerbell",
  "rainbow",
  "nathan",
  "cooper",
  "onedirection",
  "alexander",
  "jordan23",
  "lol123",
  "jasper",
  "junior",
  "q1w2e3r4",
  "222222",
  "11111111",
  "benjamin",
  "jonathan",
  "passw0rd",
  "123456789",
  "a123456",
  "samsung",
  "123",
  "love123",
];

const generateSalt = () => {
  const array = new Uint8Array(16); // 16 bajta = 128 bita
  window.crypto.getRandomValues(array);
  return Array.from(array, (dec) => ("0" + dec.toString(16)).substr(-2)).join("");
};

const pepper = "yourSecretPepper123"; // zamijenite s vašim tajnim peperom

const comparePassword = () => {
  const hasUpperCase = /[A-Z]/.test(inputPassword.value);
  const hasLowerCase = /[a-z]/.test(inputPassword.value);
  const hasSpecialChar = /[!@#$%^&*(),.?":{}|<>]/.test(inputPassword.value);
  const moreThanElevenLChar = inputPassword.value.length > 11;

  const isValidPassword =
    hasUpperCase && hasLowerCase && hasSpecialChar && moreThanElevenLChar;
  const isPasswordInList = passwordsToCompare.includes(inputPassword.value);

  check.value = isPasswordInList;

  comparisonResult.value = isValidPassword && !isPasswordInList;
};

const hashPassword = async (password) => {
  try {
    const buffer = new TextEncoder().encode(password);
    const hash = await crypto.subtle.digest("SHA-256", buffer);
    const hashedPassword = Array.from(new Uint8Array(hash))
      .map((b) => b.toString(16).padStart(2, "0"))
      .join("");

    return hashedPassword;
  } catch (error) {
    console.error("Error while hashing password:", error);
    return null;
  }
};

const handleHashing = async () => {
  encryptedPassword.value = await hashPassword(inputPassword.value);
};
</script>
