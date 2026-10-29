<template>
  <div class="mx-auto mt-10 max-w-md rounded-xl bg-white p-8 shadow-md">
    <h1 class="mb-6 text-center text-2xl font-bold text-gray-800">
      Crea Profilo
    </h1>

    <form @submit.prevent="handleRegister" class="space-y-6">
      <!-- Campo Username -->
      <div>
        <label
          for="username"
          class="mb-1 block text-sm font-medium text-gray-700"
          >Username</label
        >
        <input
          id="username"
          v-model="username"
          type="text"
          required
          placeholder="es. mario_rossi123"
          class="w-full rounded-lg border border-gray-300 px-4 py-2 outline-none focus:ring-2 focus:ring-blue-500"
        />
        <!-- Feedback Username -->
        <ul class="mt-2 space-y-1 text-xs">
          <li :class="usernameMinLength ? 'text-green-600' : 'text-gray-500'">
            {{ usernameMinLength ? '✓' : '○' }} Minimo 3 caratteri
          </li>
          <li :class="usernameValidChars ? 'text-green-600' : 'text-gray-500'">
            {{ usernameValidChars ? '✓' : '○' }} Solo lettere, numeri e
            underscore (_)
          </li>
        </ul>
      </div>

      <!-- Campo Password -->
      <div>
        <label
          for="password"
          class="mb-1 block text-sm font-medium text-gray-700"
          >Password</label
        >
        <input
          id="password"
          v-model="password"
          type="password"
          required
          placeholder="Inserisci password sicura"
          class="w-full rounded-lg border border-gray-300 px-4 py-2 outline-none focus:ring-2 focus:ring-blue-500"
        />
        <!-- Feedback Password -->
        <ul class="mt-2 space-y-1 text-xs">
          <li :class="passwordMinLength ? 'text-green-600' : 'text-gray-500'">
            {{ passwordMinLength ? '✓' : '○' }} Minimo 8 caratteri
          </li>
          <li :class="passwordHasNumber ? 'text-green-600' : 'text-gray-500'">
            {{ passwordHasNumber ? '✓' : '○' }} Almeno un numero (0-9)
          </li>
          <li :class="passwordHasSymbol ? 'text-green-600' : 'text-gray-500'">
            {{ passwordHasSymbol ? '✓' : '○' }} Almeno un simbolo speciale
            (!@#$%^&*)
            <!-- :class -colora il testo diventa verde quando l'utente digita il carattere corretto-->
          </li>
        </ul>
      </div>

      <!-- Pulsante Submit -->
      <!-- :disabled sul pulsante impedisce l'invio(anche quando viene premuto da tastiera) se isFormValid è falso. -->
      <button
        type="submit"
        :disabled="!isFormValid"
        :class="
          isFormValid
            ? 'cursor-pointer bg-blue-600 hover:bg-blue-700'
            : 'cursor-not-allowed bg-gray-400'
        "
        class="w-full rounded-lg px-4 py-2.5 font-semibold text-white transition"
      >
        Registrati
      </button>
    </form>
  </div>
</template>
<script setup lang="ts">
import { ref, computed } from 'vue'

const router = useRouter()
const username = ref('')
const password = ref('')

// Regole Username: Solo lettere, numeri, underscore e minimo 3 caratteri
const usernameMinLength = computed(() => username.value.length >= 3)
const usernameValidChars = computed(
  () => /^[a-zA-Z0-9_]*$/.test(username.value) && username.value.length > 0
)
const isUsernameValid = computed(
  () => usernameMinLength.value && usernameValidChars.value
)

// Regole Password: Minimo 8 caratteri, almeno un numero, almeno un simbolo speciale
const passwordMinLength = computed(() => password.value.length >= 8)
const passwordHasNumber = computed(() => /\d/.test(password.value))
const passwordHasSymbol = computed(() =>
  /[!@#$%^&*(),.?":{}|<>]/.test(password.value)
) // Le espressioni regolari (/^[a-zA-Z0-9_]*$/ e /\d/) controllano i caratteri inseriti: bloccano spazi o simboli strani nell'username e forzano la presenza di numeri e simboli speciali nella password.
const isPasswordValid = computed(
  () =>
    passwordMinLength.value &&
    passwordHasNumber.value &&
    passwordHasSymbol.value
)

// Validazione Globale Form
const isFormValid = computed(
  () => isUsernameValid.value && isPasswordValid.value
)

const handleRegister = () => {
  if (!isFormValid.value) return
  if (username.value === 'vale' && password.value === 'vale12345.') {
    router.push('/')
  }
}
</script>
