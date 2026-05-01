<template>
  <div>
    <header
      class="-mt-10 sticky top-0 z-50 w-full bg-white/60 backdrop-blur-md border-b border-slate-200/50"
    >
      <nav
        class="flex items-center w-[80vw] mx-auto justify-between text-gray-600 font-bold"
      >
        <ul class="">
          <li>
            <a href="">
              <img class="h-[12vh]" src="/dark.icon.png" alt="" />
            </a>
          </li>
        </ul>
        <ul class="flex items-center gap-8">
          <li v-for="link in navLinks">
            <button
              @click="scrollToSection(link.section)"
              class="hover:bg-slate-200 px-4 py-2 rounded-lg"
            >
              {{ link.name }}
            </button>
          </li>
        </ul>
        <div class="flex items-center gap-5">
          <div class="relative cursor-pointer">
            <button class="cursor-pointer" @click="toggleMode">
              <Moon v-show="activeMode == 'dark'" class="text-slate-950" />
              <Sun v-show="activeMode == 'light'" class="text-orange-500" />
              <MonitorCheck
                v-show="activeMode == 'device'"
                class="text-slate-950"
              />
            </button>
            <ul
              :class="[isShowMode ? 'flex' : 'hidden']"
              class="absolute flex-col gap-2 border border-slate-200 w-50 bg-white"
            >
              <li @click="selectMode('light')" class="hover:bg-slate-200">
                Yorug'
              </li>
              <li @click="selectMode('dark')" class="hover:bg-slate-200">
                Qorong'u
              </li>
              <li @click="selectMode('device')" class="hover:bg-slate-200">
                Qurilma
              </li>
            </ul>
          </div>
          <div class="cursor-pointer relative">
            <button class="cursor-pointer" @click="toggle">
              <Globe />
            </button>
            <ul
              :class="[isShow ? 'flex' : 'hidden']"
              class="absolute flex-col gap-2 border border-slate-200 w-50 bg-white"
            >
              <li @click="select()" class="hover:bg-slate-200">Uzb</li>
              <li @click="select()" class="hover:bg-slate-200">Rus</li>
              <li @click="select()" class="hover:bg-slate-200">Eng</li>
            </ul>
          </div>
        </div>
      </nav>
    </header>
    <div
      class="bg-slate-50 w-full min-h-[42vw] text-center flex items-center flex-col leading-tight pt-40"
    >
      <p class="text-green-400 text-[20px] font-bold">Salom, men</p>
      <h1 class="text-slate-800 font-extrabold text-[80px] mt-8">
        Muhammad Ali
      </h1>
      <p class="text-green-400 text-[30px] font-bold mt-4">
        Junior Frontend Dasturchi
      </p>
      <p class="text-[18px] font-medium text-gray-600 max-w-2xl mt-6">
        1+ yilik vue.js tajribasiga ega Frontend dasturchi. Startaplar va yirik
        <br />
        kompaniyalar uchun zamonaviy, foydalanuvchilarga qulay web ilovalar
        yarataman.
      </p>
      <div class="flex justify-center gap-8 mt-20">
        <button
          class="px-8 py-3 text-base rounded-lg font-semibold shadow-md bg-green-500 hover:bg-green-400 cursor-pointer"
        >
          Loyihalarimni ko'rish <span>&rarr;</span>
        </button>
        <button
          class="px-6 py-3 rounded-lg text-base gap-4 border border-slate-200 hover:bg-slate-100 font-semibold cursor-pointer"
        >
          Bog'lanish
        </button>
      </div>
    </div>
    <div
      id="about"
      class="flex flex-col md:flex-row items-center gap-12 lg:gap-16"
    >
      <div class="px-20 mt-20 md:w-1/2">
        <div>
          <p class="text-4xl font-bold text-slate-900 mb-20">Men xaqimda</p>
          <p class="text-slate-600 max-w-2xl text-[18px] font-medium mt-6">
            Men Muhammad Ali — 1+ yillik tajribaga ega Junior Frontend
            dasturchiman. Asosan Vue 3,TypeScript texnologiyalarida ishlayman va
            production darajasidagi web ilovalarni yaratishga ixtisoslashganman.
          </p>
          <p class="text-slate-600 max-w-2xl text-[18px] font-medium mt-6">
            Hozirda turli startaplar va kompaniyalar bilan hamkorlik qilib,
            ularning g'oyalarini hayotga tatbiq etishda yordam beraman. Shu
            bilan birga, IT-LINE Academy'da frontend bo'yicha o'qiyman.
            Kelajakda backend tomoniga ham o'sishni maqsad qilganman: hozirda
            backendni malum miqdorini ni o'rganib yuraman.
          </p>
        </div>
        <p class="text-3xl font-bold text-slate-900 mb-20 mt-8">
          Ishlaydigan texnologiyalarim:
        </p>
        <ul class="flex gap-3 mb-10">
          <li class="px-5 py-2 rounded-full bg-green-400/30 text-green-500">
            Vue 3
          </li>
          <li class="px-5 py-2 rounded-full bg-green-400/30 text-green-500">
            Git
          </li>
          <li class="px-5 py-2 rounded-full bg-green-400/30 text-green-500">
            Tailwind css
          </li>
        </ul>
      </div>
      <div class="md:w-1/2 flex justify-center">
        <img
          class="w-full max-w-120 rounded-xl shadow-2xl shadow-slate-200"
          src="data:image/jpeg;base64,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"
          alt=""
        />
      </div>
    </div>

    <div id="experience" class="max-w-4xl mx-auto px-6 py-20">
      <h2 class="text-4xl text-center font-bold text-slate-900 mb-10">
        Tajriba
      </h2>
      <h2 class="text-center text-grey-600 mb-16 text-[20px]">Kasbiy yo'lim</h2>

      <div class="relative border-l-2 border-green-400 ml-4">
        <div v-for="exp in experiences" class="mb-12 ml-8 relative">
          <div
            class="absolute -left-10.25 w-4 h-4 bg-white border-4 border-green-400 rounded-full"
          ></div>

          <div
            class="bg-white border border-slate-100 hover:border-green-400 p-8 rounded-2xl shadow-sm"
          >
            <div class="flex flex-col md:flex-row justify-between mb-4">
              <div>
                <h3 class="text-xl font-bold text-slate-900">{{ exp.role }}</h3>
                <div class="flex items-center gap-3 mt-2">
                  <span class="text-emerald-500 font-bold">{{
                    exp.company
                  }}</span>
                  <span
                    class="px-3 py-1 bg-emerald-50 text-green-400 text-xs rounded-full font-semibold"
                  >
                    {{ exp.type }}
                  </span>
                  <span class="text-slate-400 text-sm">{{ exp.location }}</span>
                </div>
              </div>
              <div class="text-slate-400 text-sm mt-2">
                {{ exp.date }}
              </div>
            </div>
            <p class="text-gray-600">
              {{ exp.description }}
            </p>
          </div>
        </div>
      </div>
    </div>
    <div class="px-20 mt-20 -my-20">
      <h2 class="text-4xl font-bold text-slate-900 mb-10">Loyihalar</h2>
      <div class="flex justify-between">
        <p class="text-grey-600 mb-16 text-[20px]">So'nggi ishlarim</p>

        <button class="text-green-400 text-[22px] hover:underline -my-60">
          Barcha loyihalarim <span> &rarr;</span>
        </button>
      </div>
    </div>
    <div id="projects" class="px-10 mt-30 flex justify-center gap-10">
      <div
        class="border border-slate-200 p-6 rounded-2xl cursor-pointer max-w-sm flex flex-col shadow-sm hover:border-green-400 hover:text-green-400"
      >
        <img
          class="w-full h-52 rounded-xl bg-slate-100"
          src="/Xarajat.png"
          alt="xarajat-app.vercel.app"
        />

        <div class="mt-6 flex items-center gap-3">
          <h3 class="text-[20px] font-bold">Xarajat</h3>
          <span
            class="px-3 py-1 rounded-full bg-green-400/20 text-green-600 text-[12px] font-bold"
            >STARTUP</span
          >
        </div>

        <p class="mt-4 text-[16px] text-slate-600 leading-relaxed">
          Turli imtihonlar uchun AI baholash bilan mock test platformasi: IELTS,
          CEFR, DTM va boshqalar. Speaking...
        </p>

        <div class="flex gap-2 mt-6">
          <span
            class="px-3 py-1 rounded-full bg-slate-100 text-slate-700 text-sm font-semibold"
            >Vue 3</span
          >
          <span
            class="px-3 py-1 rounded-full bg-slate-100 text-slate-700 text-sm font-semibold"
            >Vite</span
          >
          <span
            class="px-3 py-1 rounded-full bg-slate-100 text-slate-700 text-sm font-semibold"
            >TypeScript</span
          >
        </div>

        <a
          href="https://xarajat-ilzdxn5a2-alinematov0102-stacks-projects.vercel.app"
          target="_blank"
          rel="noopener noreferrer"
          class="hover:underline mt-6 text-green-600 font-bold text-left"
        >
          Jonli ko'rish
        </a>
      </div>

      <div
        class="border border-slate-200 p-6 rounded-2xl cursor-pointer max-w-sm flex flex-col shadow-sm hover:border-green-400 hover:text-green-400"
      >
        <img
          class="w-full h-52 object-cover rounded-xl bg-slate-100"
          src="/calculator.png"
          alt=""
        />

        <div class="mt-6 flex items-center gap-3">
          <h3 class="text-[20px] font-bold">Calculator</h3>
          <span
            class="px-3 py-1 rounded-full bg-green-400/20 text-green-600 text-[12px] font-bold"
            >STARTUP</span
          >
        </div>

        <p class="mt-4 text-[16px] text-slate-600 leading-relaxed">
          Ishlab chiqarish uchun universal ERP tizimi. 6 ta integratsiyalangan
          modul: HR va tabel, ombor va...
        </p>

        <div class="flex gap-2 mt-6">
          <span
            class="px-3 py-1 rounded-full bg-slate-100 text-slate-700 text-sm font-semibold"
            >Vue 3</span
          >
          <span
            class="px-3 py-1 rounded-full bg-slate-100 text-slate-700 text-sm font-semibold"
            >Nuxt 3</span
          >
          <span
            class="px-3 py-1 rounded-full bg-slate-100 text-slate-700 text-sm font-semibold"
            >TypeScript</span
          >
        </div>

        <a
          class="hover:underline mt-6 text-green-600 font-bold text-left"
          href="https://calculator-7xln4u69j-alinematov0102-stacks-projects.vercel.app"
          target="_blank"
          rel="noopener noreferrer"
        >
          Jonli ko'rish</a
        >
      </div>

      <div
        class="border border-slate-200 p-6 rounded-2xl cursor-pointer max-w-sm flex flex-col shadow-sm hover:border-green-400 hover:text-green-400"
      >
        <img
          class="w-full h-52 object-cover rounded-xl bg-slate-100"
          src="/amalyot.png"
          alt="ToDo"
        />

        <div class="mt-6 flex items-center gap-3">
          <h3 class="text-[20px] font-bold">To-do-List</h3>
          <span
            class="px-3 py-1 rounded-full bg-green-400/20 text-green-600 text-[12px] font-bold"
            >STARTUP</span
          >
        </div>

        <p class="mt-4 text-[16px] text-slate-600 leading-relaxed">
          O'zbekistondagi 500+ kompaniyadan chegirmalarni yig'uvchi Telegram
          Mini App. Tangalar bilan QR kod...
        </p>

        <div class="flex gap-2 mt-6">
          <span
            class="px-3 py-1 rounded-full bg-slate-100 text-slate-700 text-sm font-semibold"
            >Vue 3</span
          >
          <span
            class="px-3 py-1 rounded-full bg-slate-100 text-slate-700 text-sm font-semibold"
            >Vite</span
          >
          <span
            class="px-3 py-1 rounded-full bg-slate-100 text-slate-700 text-sm font-semibold"
            >TypeScript</span
          >
        </div>

        <a
          href="https://todo-a06fkgpvc-alinematov0102-stacks-projects.vercel.app"
          target="_blank"
          rel="noopener noreferrer"
          class="hover:underline mt-6 text-green-600 font-bold text-left"
        >
          Jonli ko'rish
        </a>
      </div>
    </div>
    <div class="px-20 mt-20 -my-20">
      <h2 class="text-4xl font-bold text-slate-900 mb-10">Maqolalar</h2>
      <div class="flex justify-between">
        <p class="text-grey-600 mb-16 text-[20px]">
          Dasturlash haqida fikrlarim
        </p>

        <button
          class="text-green-500 text-[22px] flex gap-2 hover:underline font-semibold"
        >
          Barcha maqolalar <span> &rarr;</span>
        </button>
      </div>
    </div>
    <div id="articles" class="mt-20 mx-10 px-20">
      <div class="flex gap-8">
        <div
          class="border border-slate-200 rounded-3xl px-10 py-8 max-w-sm flex flex-col gap-5 shadow-sm hover:border-green-400 hover:text-green-400"
        >
          <div>
            <p
              class="inline-block px-4 py-2 rounded-full bg-emerald-50 text-green-400 font-semibold"
            >
              golang
            </p>
          </div>

          <h2 class="text-[22px] font-bold">
            Learning Go: O'rnatish va Go Vositalari
          </h2>

          <p class="text-gray-600 text-[18px]">
            Jon Bodnerning 'Learning Go (Second Edition)' kitobidan o'rnatish
            bo'limi bo'yicha xulosalar - go fmt,...
          </p>

          <div class="border-t border-slate-200 pt-4">
            <p class="text-slate-400 text-[18px]">19.12.2025</p>
          </div>
        </div>
        <div
          class="border border-slate-200 rounded-3xl px-10 py-8 max-w-sm flex flex-col gap-5 shadow-sm hover:border-green-400 hover:text-green-400"
        >
          <div>
            <p
              class="inline-block px-4 py-2 rounded-full bg-emerald-50 text-green-400 font-semibold"
            >
              golang
            </p>
          </div>

          <h2 class="text-[22px] font-bold">
            Learning Go: Ma'lumot Turlari (Types)
          </h2>

          <p class="text-gray-600 text-[18px]">
            Jon Bodnerning 'Learning Go (Second Edition)' kitobidan ma'lumot
            turlari bo'yicha xulosalar - static...
          </p>

          <div class="border-t border-slate-200 pt-4">
            <p class="text-slate-400 text-[18px]">19.12.2025</p>
          </div>
        </div>
      </div>
    </div>
    <div id="contact" class="mt-30 mx-10 flex flex-col">
      <div class="text-center">
        <p class="text-[30px] font-bold">Bog'lanish</p>
        <p class="text-[20px] text-gray-600 mt-10">
          Men bilan bog'laning! Savollaringiz yoki takliflaringiz bo'lsa,
          bemalol yozing.
        </p>
      </div>
      <div class="mt-15">
        <div class="flex justify-center items-center gap-8">
          <div
            class="border border-slate-200 max-w-md rounded-2xl px-10 py-5 flex gap-2"
          >
            <p
              class="inline-block px-5 py-5 rounded-full bg-emerald-50 text-green-400"
            >
              <Mail />
            </p>
            <div class="">
              <p class="text-[18px] text-gray-600">Electron pochta</p>
              <a class="hover:text-green-600 text-[20px] font-bold" href=""
                >Muhammadali_210@gmail.com</a
              >
            </div>
          </div>
          <div
            class="border border-slate-200 max-w-md rounded-2xl px-10 py-5 flex gap-2"
          >
            <p
              class="inline-block px-5 py-5 rounded-full bg-emerald-50 text-green-400"
            >
              <MapPin />
            </p>
            <div class="">
              <p class="text-[18px] text-gray-600">Manzil</p>
              <a class="hover:text-green-600 text-[20px] font-bold" href=""
                >Qo'qon, Farg'ona, O'zbekiston</a
              >
            </div>
          </div>
        </div>
        <div class="flex justify-center items-center mt-10">
          <button
            class="flex items-center gap-2 px-10 py-5 text-[20px] rounded-lg font-semibold shadow-md bg-green-400 cursor-pointer"
          >
            <Send class="w-5 h-5" /> Loyihalarimni ko'rish
          </button>
        </div>
      </div>
    </div>
    <section class="w-screen h-110">
      <div class="border-t border-slate-200 pt-16 mt-30">
        <div class="flex justify-center items-start gap-60">
          <div class="flex flex-col gap-5 max-w-md">
            <img class="h-40 w-54" src="/dark.icon.png" alt="" />

            <p class="text-grey-600 text-[20px] font-semibold">
              Vue 3 va zamonaviy frontend texnologiyalari yordamida ajoyib
              raqamli tajribalar yaratuvchi Junior Frontend dasturchi.
            </p>

            <div class="flex items-center gap-7">
              <button
                class="cursor-pointer hover:text-black hover:px-2 py-2 hover:bg-slate-200 hover:rounded-lg"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="32"
                  height="32"
                  viewBox="0 0 24 24"
                >
                  <g
                    fill="none"
                    stroke="#94A3B8"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="1.5"
                  >
                    <path
                      d="M3.5 15.668q.675.081 1 .618c.326.537 1.537 2.526 2.913 2.526H9.5m5.672-3.513q.823 1.078.823 1.936V21m-5.625-5.609q-.87.954-.869 1.813V21"
                    />
                    <path
                      d="M15.172 15.299c1.202-.25 2.293-.682 3.14-1.316c1.448-1.084 2.188-2.758 2.188-4.411c0-1.16-.44-2.243-1.204-3.16c-.425-.511.819-3.872-.286-3.359c-1.105.514-2.725 1.198-3.574.947c-.909-.268-1.9-.416-2.936-.416c-.9 0-1.766.111-2.574.317c-1.174.298-2.296-.363-3.426-.848c-1.13-.484-.513 3.008-.849 3.422C4.921 7.38 4.5 8.44 4.5 9.572c0 1.653.895 3.327 2.343 4.41c.965.722 2.174 1.183 3.527 1.41"
                    />
                  </g>
                </svg>
              </button>
              <button
                class="cursor-pointer hover:text-slate-950 hover:px-2 py-2 hover:bg-slate-200 hover:rounded-lg"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="32"
                  height="32"
                  viewBox="0 0 24 24"
                >
                  <g
                    fill="none"
                    stroke="#94A3B8"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                  >
                    <circle cx="4" cy="4" r="2" />
                    <path
                      d="M2 9h4v12H2Zm20 12h-4v-7a2 2 0 0 0-4 0v7h-4v-7a6 6 0 0 1 12 0Z"
                    />
                  </g>
                </svg>
              </button>
              <button
                class="cursor-pointer hover:text-slate-950 hover:px-2 py-2 hover:bg-slate-200 hover:rounded-lg"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="32"
                  height="32"
                  viewBox="0 0 24 24"
                >
                  <g fill="none" stroke="#94A3B8" stroke-width="1.5">
                    <path
                      fill="yellow"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      d="m14 12l-3.5 2v-4z"
                    />
                    <path
                      d="M2 12.708v-1.416c0-2.895 0-4.343.905-5.274c.906-.932 2.332-.972 5.183-1.053C9.438 4.927 10.818 4.9 12 4.9s2.561.027 3.912.065c2.851.081 4.277.121 5.182 1.053S22 8.398 22 11.292v1.415c0 2.896 0 4.343-.905 5.275c-.906.931-2.331.972-5.183 1.052c-1.35.039-2.73.066-3.912.066s-2.561-.027-3.912-.066c-2.851-.08-4.277-.12-5.183-1.052S2 15.602 2 12.708Z"
                    />
                  </g>
                </svg>
              </button>
              <button
                class="cursor-pointer hover:text-slate-950 hover:px-2 py-2 hover:bg-slate-200 hover:rounded-lg"
              >
                <Send class="text-slate-400" />
              </button>
            </div>
          </div>

          <!-- CENTER -->
          <div class="flex flex-col gap-3">
            <p class="text-slate-900 font-bold text-[20px]">BO'LIMLAR</p>
            <a
              class="text-gray-600 hover:text-black font-semibold text-[18px]"
              href=""
              >Men haqimda</a
            >
            <a
              class="text-gray-600 hover:text-black font-semibold text-[18px]"
              href=""
              >Tajriba</a
            >
            <a
              class="text-gray-600 hover:text-black font-semibold text-[18px]"
              href=""
              >Loyihalar</a
            >
          </div>

          <!-- RIGHT -->
          <div class="flex flex-col gap-3">
            <p class="text-slate-900 font-bold text-[20px]">MANBALAR</p>
            <a
              class="text-gray-600 hover:text-black font-semibold text-[18px]"
              href=""
              >Maqolalar</a
            >
            <a
              class="text-gray-600 hover:text-black font-semibold text-[18px]"
              href=""
              >Hujjatlar</a
            >
            <a
              class="text-gray-600 hover:text-black font-semibold text-[18px]"
              href=""
              >Aloqa</a
            >
          </div>
        </div>

        <div class="mt-16 pt-6 border-t px-20 border-slate-200"></div>
        <p class="text-center text-slate-400 text-sm">
          © 2026 Muhammad Ali. Barcha huquqlar himoyalangan.
        </p>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref } from "vue";
import {
  Moon,
  Globe,
  Sun,
  MonitorCheck,
  Mail,
  MapPin,
  Send,
} from "lucide-vue-next";
let isShowMode = ref(false);
let isShow = ref(false);
let active = ref("Uzb");
let activeMode = ref("device");
let navLinks = [
  { id: 1, name: "Men haqimda", section: "about" },
  { id: 2, name: "Tajriba", section: "experience" },
  { id: 3, name: "Loyihalar", section: "projects" },
  { id: 4, name: "Maqolalar", section: "articles" },
  { id: 5, name: "Aloqa", section: "contact" },
];
function scrollToSection(id) {
  const el = document.getElementById(id);
  if (el) {
    const yOffset = -100; // header balandligi
    const y = el.getBoundingClientRect().top + window.pageYOffset + yOffset;

    window.scrollTo({
      top: y,
      behavior: "smooth",
    });
  }
}
function toggle() {
  isShow.value = !isShow.value;
}
function toggleMode() {
  isShowMode.value = !isShowMode.value;
}
function select(id) {
  active.value = id;
  isShow.value = !isShow.value;
}
function selectMode(id) {
  activeMode.value = id;
  isShowMode.value = !isShowMode.value;
}
let experiences = ref([
  {
    id: 1,
    role: "Frontend Dasturchi",
    company: "It-line",
    type: "Full-time",
    location: "Qo'qon, Farg'ona",
    date: "2025.06 - Hozir",
    description:
      "Kompaniyaning hammuassisi va frontend yo'nalish rahbari. Startap va biznes loyihalarida Vue 3, bilan frontend ishlab chiqarish. Tizimli ERP, AI-integratsiyalar, JWT refresh queue kabi murakkab texnik yechimlarni amalga oshirdim.",
  },
  {
    id: 2,
    role: "Frontend Mentor",
    company: "IT-LINE ACADEMY",
    type: "Part-time",
    location: "Qo'qon, Farg'ona",
    date: "2024.07 - Hozir",
    description:
      "150+ o'quvchiga kompyuter savodxonligi va frontend dasturlash (Vue 3) bo'yicha dars oldim. O'rta darajadagi guruhlarga TypeScript, state management va clean code prinsiplarini o'rgandim. Vue 3 Composition API bo'yicha o'zbekcha darslarda qatnashtim.",
  },
  {
    id: 3,
    role: "Frontend Dasturchi",
    company: "Online Service Group",
    type: "Part-time",
    location: "Remote",
    date: "2024.05 - 2024.12",
    description:
      "Vue 3, Vuetify yordamida davlat platformalari uchun admin panellar va interfeyslar ishlab chiqish. Rol asosidagi kirish nazorati (RBAC), forma validatsiyasi, SEO-kritik sahifalar uchun SSR implementatsiyasini organdim.",
  },
]);
</script>

<style scoped>
[id] {
  scroll-margin-top: 120px;
}
</style>
