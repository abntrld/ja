<template>
  <main class="min-h-screen flex flex-col items-center justify-center bg-pink-50 text-pink-900">
    <!-- Welcome / Password page -->
    <div v-if="!isUnlocked" class="bg-beige-100 p-8 rounded-2xl shadow-md text-center w-80">
      <h1 class="text-3xl font-bold mb-4">привет жан 😛</h1>
      <p class="mb-4 text-pink-700">пароль пожалуйста 🤗</p>
      <input
        v-model="password"
        @keyup.enter="checkPassword"
        type="password"
        placeholder="dd.mm.yyyy"
        class="border border-rose-300 rounded-md px-3 py-2 mb-4 w-full text-center"
      />
      <button
        @click="checkPassword"
        class="bg-rose-500 hover:bg-rose-600 text-white font-medium px-4 py-2 rounded-md w-full transition"
      >
        Открыть 💌
      </button>
      <p v-if="error" class="text-red-500 mt-3 text-sm">Неправильная дата😤</p>
    </div>

    <!-- Story page -->
    <div v-else class="text-center p-6 animate-fadeIn">
      <h1 class="text-4xl font-bold mb-6">добро пожаловать</h1>
      <p class="mb-8">мой небольшой подарочек🌷</p>

      <section class="w-full max-w-5xl mx-auto px-4 py-12">
        <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-8">
          <div
          v-for="(memory, index) in memories"
          :key="index"
          class="bg-white rounded-lg shadow-md border border-rose-200 overflow-hidden transform transition hover:-translate-y-2 hover:shadow-xl"
          >
      <!-- Photo -->
      <img
        v-if="memory.photo"
        :src="memory.photo"
        alt="memory photo"
        class="w-full h-30 object-cover"
      />

      <div class="p-4">
        <!-- Date -->
        <span class="inline-block bg-rose-100 text-rose-700 px-3 py-1 rounded-full text-sm font-medium mb-2">
          {{ memory.date }}
        </span>

        <!-- Text -->
        <p class="text-rose-700 mt-2">{{ memory.text }}</p>
      </div>
    </div>
  </div>
  <div class="mt-12 font-serif text-center text-rose-800 italic text-lg leading-relaxed tracking-wide">
        <p>
          так странно от понимания что первый курс был два года назад. так сложно
        принять что нашим отношениям уже два года. за эти два года наши
        отношения прошли через многое. в том плане что, мы буквально все вместе
        пережили. помню как мы только начинали сближаться, помню первую бутылку
        воды; помню первые сообщения и первые взгляды. это все происходило так
        быстро что хотелось на дольше растянуть это время и побыть подольше в
        этих чувствах. в особенности первые дни, когда мы лежали друг против
        друга - смотря друг на друга. с того момента поняла что ты мой человек и
        было все равно что мы почти и не говорили, но мы чувствовали. иногда я
        забываю тебя благодарить за то что всегда слушаешь меня, говоришь да на
        все мои запросы и желания, ставишь меня в приоритеты даже если у тебя
        плотный график, заботишься обо мне когда я чувствую себя плохо и спасибо
        что ты делаешь для меня. спасибо тебе большое, жан. спасибо за то что ты
        и есть тот самый мужчина о котором я даже мечтать не могла. спасибо что
        всегда слушаешь мои истории и даже самые тупые и не смешные истории.
        спасибо за то что ты всегда рядом тогда когда я нуждаюсь в этом больше
        всего. слов даже не хватит описать насколько я удачлива и благодарна за
        то что ты есть в моей жизни. может я и не самая идеальная и не самая
        лучшая девушка на этом свете но я правда люблю тебя всем сердцем и
        душой. может я и проиграла в некоторых аспектах но я выиграла то о чем я
        даже и не думала. встретить тебя - это было самое лучшее событие в моей
        жизни, и выбрать любить тебя - был самый лучший выбор который я когда
        либо делала. спасибо что выбрал меня, я всегда буду рядом и за тобой.
        помни что у тебя всегда есть я. я буду всегда любить тебя в твои
        тяжелые дни. тебе не нужно притворяться что у тебя все хорошо даже когда
        нет. ты - самый лучший человек которого я когда либо встречала, и самое
        лучшее что со мной происходило.
        </p>
        
        <div class="mt-8 text-center text-sm text-rose-600 italic">
      <p>
        thank you for treating me better from my past. thank you for healing me.
        thank you for trusting me and for giving me your trust. thank you for
        matching my energy and thank you for being the best. i love you so much
      </p>
    </div>
      </div>
</section>

      <footer class="mt-10 text-sm text-rose-700">
        Made with love by Adinka
      </footer>

      <button
      @click="lockAgain"
      class="mt-6 text-sm text-rose-600 underline hover:text-rose-800"
      >
      Закрыть 🔒
      </button>
    </div>
  </main>
</template>

<script setup>
import { ref, onMounted } from 'vue'

// your special date password 💞
const correctPassword = '19.11.2023'

const password = ref('')
const isUnlocked = ref(false)
const error = ref(false)

const checkPassword = () => {
  if (password.value.trim() === correctPassword) {
    isUnlocked.value = true
    error.value = false
    localStorage.setItem('unlocked', 'true') // remember access
  } else {
    error.value = true
  }
}

const lockAgain = () => {
  localStorage.removeItem('unlocked')
  isUnlocked.value = false
}

// Check if already unlocked before
onMounted(() => {
  const saved = localStorage.getItem('unlocked')
  if (saved === 'true') {
    isUnlocked.value = true
  }
})

const memories = [
  { 
    date: '2023-11-19', 
    text: 'день когда мы начали встречаться', 
    photo: '/images/19.11.png' 
  },
  { 
    date: '2023-12-28', 
    text: 'первый раз вместе в астане', 
    photo: '/images/28.12.png' 
  },
  { 
    date: '2024-01-15', 
    text: 'дни нашей разлуки на каникулы', 
    photo: '/images/15.01.2024.png' 
  },
  { 
    date: '2024-03-08', 
    text: 'восьмое мартааа💞', 
    photo: '/images/08.03.2024.png' 
  },
  { 
    date: '2024-04-16', 
    text: 'наш второй трип в астану', 
    photo: '/images/16.04.2024.png' 
  },
  { 
    date: '2024-04-20', 
    text: 'моя дршкаа', 
    photo: '/images/20.04.2024.png' 
  },
  { 
    date: '2024-04-22', 
    text: 'наши гулянки в астанееее', 
    photo: '/images/22.04.2024.png' 
  },
  { 
    date: '2024-04-26', 
    text: 'твоя дршкаа', 
    photo: '/images/26.04.2024.png' 
  },
  { 
    date: '2024-05-26', 
    text: 'отмечали полгодааа', 
    photo: '/images/26.05.2024.png' 
  },
  { 
    date: '2024-06-04', 
    text: 'страдали фигней во время нашей первой практики', 
    photo: '/images/04.06.2024.png' 
  },
  { 
    date: '2024-06-13', 
    text: 'и опять разлукааа', 
    photo: '/images/13.06.2024.png' 
  },
  { 
    date: '2024-06-18', 
    text: 'уехал', 
    photo: '/images/18.06.2024.png' 
  },
  { 
    date: '2024-06-26', 
    text: 'первые цветочки на расстоянии', 
    photo: '/images/26.06.2024.png' 
  },
  { 
    date: '2024-08-07', 
    text: 'приехаал', 
    photo: '/images/07.08.2024.png' 
  },
  { 
    date: '2024-11-19', 
    text: 'целый год', 
    photo: '/images/19.11.2024.png' 
  },
  { 
    date: '2024-12-08', 
    text: 'любили делать маски', 
    photo: '/images/08.12.2024.png' 
  },
  { 
    date: '2024-12-28', 
    text: 'вот так вот мы и встречали новый год', 
    photo: '/images/28.12.2024.png' 
  },
  { 
    date: '2025-01-30', 
    text: 'начался второй семестр ВТОРОГО курса', 
    photo: '/images/30.01.2025.png' 
  },
  { 
    date: '2025-02-15', 
    text: 'awwww my shaylaaa то как ты мне приносил кофе в постель', 
    photo: '/images/15.02.2025.png' 
  },
  { 
    date: '2025-03-08', 
    text: 'awww восьмое марта уже как второй год', 
    photo: '/images/08.03.2025.png' 
  },
  { 
    date: '2025-04-19', 
    text: 'наш второй концерт и мой самый любимый концерт', 
    photo: '/images/19.04.2025.png' 
  },
  { 
    date: '2025-04-20', 
    text: 'моя дршкааа', 
    photo: '/images/20.04.2025.png' 
  },
  { 
    date: '2025-26-04', 
    text: 'твоя дршкааа', 
    photo: '/images/26.04.2025.png' 
  },
  { 
    date: '2025-09-07', 
    text: 'после долгой разлуки аж на три месяца', 
    photo: '/images/08.09.2025.png' 
  },

];
</script>

<style>
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-fadeIn {
  animation: fadeIn 0.8s ease forwards;
}
</style>