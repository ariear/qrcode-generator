<template>
  <div class="h-screen flex flex-col justify-center items-center bg-slate-800">
      <div class="font-pupylinux bg-white py-7 w-[90vw] md:w-[600px] text-center rounded-lg transition-all" :class="hasil ? 'h-[500px] md:h-[450px]' : 'h-[190px]' ">
          <p class="font-semibold text-xl">QR Code Generator</p>
          <form @submit.prevent="mengqr">
          <div v-if="!hasil">
          <input type="text" v-model="input" class="border py-2 px-3 rounded-lg mt-7 mr-4" placeholder="Paste your url here">
          <button type="submit" class="bg-blue-400 py-2 px-4 rounded-xl text-white md:mt-0 mt-3">Generate</button>
          </div>
          </form>
          <button v-if="hasil" class="py-2 px-5 text-white rounded-lg mt-7 bg-green-400"><a :href="qr" download="qrcode">Download Qr</a></button>
          <img v-if="hasil" :src="qr" class="mx-auto mt-8" alt="">
      </div>
      
      <a href="https://github.com/Arie75/qrcode-generator" class="absolute w-[50px] md:w-[70px] bg-white rounded-full right-7 md:right-12 bottom-12"><img src="/img/github.png" alt=""></a>
  </div>
</template>

<script>
import { ref } from 'vue'
export default {
    setup() {
        const input = ref('')
        const qr = ref('')
        const hasil = ref(false)

        const mengqr = async () => {
            qr.value = `https://api.qrserver.com/v1/create-qr-code/?data=${input.value}&amp;size=200x200`
            hasil.value = true
            input.value = ''
        }

        return { qr , input , mengqr , hasil }
    }
}
</script>