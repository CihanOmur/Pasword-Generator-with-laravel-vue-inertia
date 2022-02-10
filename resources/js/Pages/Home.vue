<template>
  <div class="">
    <div class="w-1/2 m-auto text-center bg-gray-300 py-10">
      <h1 class="text-5xl font-extralight">Password Generator</h1>
    </div>
    <div class="m-auto w-1/2 bg-gray-300">
        <div class="w-1/2 m-auto text-center bg-gray-300">
        <input v-model="password" ref="clone" v-on:focus="$event.target.select()" type="text" class="border border-red-400 rounded-md h-10 w-full">
        <button @click="yenile" class="bg-green-600 py-2 px-3 mt-3 mx-2 border-green-800 rounded-md hover:bg-green-500">Şifreyi Yenile</button>
        <button @click="copy" class="bg-yellow-600 py-2 px-3 mt-3 mx-2 border-yellow-800 rounded-md hover:bg-yellow-500">Şifreyi Kopyala</button>
    </div>
        <div class="w-2/3 m-auto text-center bg-gray-300 py-3">
            <div class="flex justify-around">
                <div class="bg-gray-200 px-2 rounded-md"><input type="checkbox" v-model="hasNumber" name="" id="sayilabel" /><label for="sayilabel">Sayı kullan</label></div>
                <div class="bg-gray-200 px-2 rounded-md"><input type="checkbox" v-model="hasSpecial" name="" id="sembollabel" /><label for="sembollabel">Sembol kullan</label></div>
                <div class="bg-gray-200 px-2 rounded-md"><input type="checkbox" v-model="hasString" name="" id="uppercaselabel" /><label for="uppercaselabel">Büyük harf Kullan</label></div>
            </div>
        </div>
        <div class=" text-center bg-gray-300 py-3">
            <input @change="uzunlukmet" v-model="uzunluk" type="range" class="border w-1/2 border-black rounded-md" placeholder="Uzunluğu Seçiniz" min="0" />{{ uzunluk }}
        </div>
    </div>
    
  </div>
</template>

<script>
export default {
    data() {
        return {
            hasString:false,
            hasNumber:false,
            hasSpecial:false,
            uzunluk:5
        }
    },
    computed:{
        charSet(){
            let chars = 'abcdefghijklmnopqrstuvwxyz';
            if (this.hasString) {
                chars += 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
            }
            if (this.hasNumber) {
                chars += '0123456789';
            }
            if (this.hasSpecial) {
                chars += '!#+%[]{}?*-_';
            }
            return chars ;   
        },
        password(){
             if (this.uzunluk <0  || this.uzunluk =='') {
                alert('uzunluk sec')
            }
            else{
                let pass=''
            for (var i = 0; i < this.uzunluk; i++) {
                var randomPoz = Math.floor(Math.random() * this.charSet.length);
                pass += this.charSet.substring(randomPoz,randomPoz+1);
            }
            return pass
            }

        }
    },
    methods: {
        yenile(){
            this.hasString = !this.hasString
            this.hasString = !this.hasString
        },
        copy() {
            this.$refs.clone.focus();
            document.execCommand('copy');
        }
    },
};
</script>
