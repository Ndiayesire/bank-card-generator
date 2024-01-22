<template>
  <div class="bg-gray-50 min-h-screen">
    <h1 class="text-center text-2xl font-semibold tracking-tight pt-3 text-gray-500">BANK CARD GENERATOR</h1>
    <div class="mx-auto container flex flex-col md:flex-row justify-center py-8 md:py-16 px-4">
      <div class="w-full md:w-1/2 pr-4 mb-8 md:mb-0">
        <div class="flex flex-col  ">
          <!-- card -->
          <div class="flex-grow text-white h-60 md:w-96 p-3 rounded-xl shadow transform transition duration-500 hover:scale-110" :style="{ background: selectedColor }">
            <div class="h-full flex flex-col justify-between mb-2">
              <div class="flex items-start justify-between space-x-4">
                <div class="text-xl font-semibold tracking-tight">{{ state.bank }}</div>
                <div class="inline-flex items-center justify-center" v-if="selectedFile">
                  <img :src="`/src/assets/${ selectedFile.name}`" class="h-12 rounded">
                </div>
              </div>
              <div class="flex space-x-1">
                <img src="../assets/nfc.png" class="h-8 w-15 rounded">
                <div class="inline-block w-12 h-8 bg-gradient-to-tl from-yellow-500 to-yellow-200 rounded-md shadow-inner overflow-hidden">
                  <div class="relative w-full h-full grid grid-cols-2 gap-1">
                    <div class="absolute border border-gray-900 rounded w-4 h-6 left-4 top-1"></div>
                    <div class="border-b border-r border-gray-900 rounded-br"></div>
                    <div class="border-b border-l border-gray-900 rounded-bl"></div>
                    <div class=""></div>
                    <div class=""></div>
                    <div class="border-t border-r border-gray-900 rounded-tr"></div>
                    <div class="border-t border-l border-gray-900 rounded-tl"></div>
                  </div>
                </div>
              </div>
              <div class="pt-1">
                <div class="text-xs font-semibold tracking-tight">Numéro carte</div>
                <div class="text-2xl font-mono">{{formattedCardNumber }}</div>
              </div>
              <div class="flex justify-between">
                <div class="">
                  <div class="text-xs font-semibold tracking-tight">Tiulaire de la carte</div>
                  <div class="text-xl font-semibold">{{ state.name }}</div>
                </div>
                <div class="">
                  <div class="text-xs font-semibold tracking-tight">Validité</div>
                  <div class="text-xl font-mono">{{ state.validity }}</div>
                </div>
              </div>
            </div>
          </div>

         
        </div>
        <div class="flex pt-5">
            <!--Back card -->
            <div class="text-white h-60 md:w-96 p-3 rounded-xl shadow transform transition duration-500 hover:scale-110" :style="{ background: selectedColor }">
              <p class="text-xs font-semibold tracking-tight">VOUS AVEZ RAMASSE LA CARTE CONTACTER LE SERVICE CLIENT</p>
              <div class="bg-black h-9 rounded-md"></div>
             <div class="pt-3">
              <div class="w-[14rem] bg-gray-200 h-9 rounded">
                <h1 class="text-gray-900 text-xl text-right mr-2 pt-1 italic">{{ state.cvc }}</h1>
              </div>
             </div>
             <div class="">
                <p class="text-xs tracking-tight mb-2 ">Signature Autorisée</p>
              </div>
              
            </div>
          </div>
      </div>

      <div class="w-full md:w-2/2">
        <div class="w-full max-w-lg mx-auto p-8">
          <div class="bg-white rounded-lg shadow p-6 border">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div class="col-span-2 sm:col-span-1">
                <label for="card-number" class="block text-sm font-medium text-gray-700 mb-2">Banque</label>
                <input type="text" v-model="state.bank" placeholder="Nom de la banque" class="w-full py-3 px-4 border border-gray-400 rounded-lg focus:outline-none focus:border-blue-500">
              </div>
              <div class="col-span-2 sm:col-span-1">
                <label for="card-number" class="block text-sm font-medium text-gray-700 mb-2">Numéro Carte</label>
                <input maxlength="16" type="text" v-model="state.cardNumber" placeholder="0000 0000 0000 0000" class="w-full py-3 px-4 border border-gray-400 rounded-lg focus:outline-none focus:border-blue-500">
              </div>
              <div class="col-span-2 sm:col-span-1">
                <label for="expiration-date" class="block text-sm font-medium text-gray-700 mb-2">Expiration Date</label>
                <input type="text" v-model="state.validity" @input="onValidityInput" placeholder="MM / YY" class="w-full py-3 px-4 border border-gray-400 rounded-lg focus:outline-none focus:border-blue-500">
              </div>
              <div class="col-span-2 sm:col-span-1">
                <label for="card-holder" class="block text-sm font-medium text-gray-700 mb-2">Propriétaire</label>
                <input type="text" v-model="state.name" placeholder="Nom complet" class="w-full py-3 px-4 border border-gray-400 rounded-lg focus:outline-none focus:border-blue-500">
              </div>
              <div class="col-span-2 sm:col-span-1">
                <label for="card-holder" class="block text-sm font-medium text-gray-700 mb-2">CVC</label>
                <input type="text" maxlength="3" v-model="state.cvc" placeholder="000" class="w-full py-3 px-4 border border-gray-400 rounded-lg focus:outline-none focus:border-blue-500">
              </div>
              <div class="col-span-2 sm:col-span-1">
                <label for="color-input" class="block text-sm font-medium text-gray-700 mb-2">Selectionner Couleur</label>
                <input type="color" v-model="selectedColor"  @input="updateColor" class="w-full h-[4rem] py-3 px-4 border bg-white rounded-lg focus:outline-none focus:border-blue-500" >
              </div>
             
            </div>
            <div class="flex flex-col pt-2">
         
         <label for="color-input" class="block text-sm font-medium text-gray-700 mb-2">Logo</label>
         <input type="file" class="w-full h-[4rem] py-3 px-4 border bg-white rounded-lg focus:outline-none focus:border-blue-500" @change="handleFileChange">
       </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref, watch } from 'vue'

const state = reactive({
  cardNumber: '',
  name: '',
  bank: '',
  cvc: '',
  validity:'',
})

const formattedCardNumber = ref('0000 0000 0000 0000')

watch(() => state.cardNumber, () => {
  formatCardNumber()
})

const formatCardNumber = () => {
  const rawNumber = state.cardNumber.replace(/\D/g, '').slice(0, 16);
  const formatted = rawNumber.replace(/(\d{4})/g, '$1 ').trim();
  formattedCardNumber.value = formatted;
}

const onValidityInput = () => {
  autoFormatValidity();
}

const autoFormatValidity = () => {
  let rawValidity = state.validity.replace(/\D/g, '');
  const month = rawValidity.slice(0, 2);
  const year = rawValidity.slice(2, 4);

  if (month.length === 2) {
    state.validity = `${month} / ${year}`;
  }
}

const selectedColor = ref('#rrggbb');

const updateColor = () => {
  const color = selectedColor.value;
  selectedColor.value = color;
};

const selectedFile = ref(null);

const handleFileChange = (event) => {
  const fileInput = event.target;
  const file = fileInput.files[0];

  if (file) {
    // Set the selectedFile object with file information
    selectedFile.value = {
      path: URL.createObjectURL(file), // Get a temporary URL for the file
      name: file.name,
      type: file.type,
    };
  } else {
    // Reset selectedFile if no file is selected
    selectedFile.value = null;
  }
};
</script>

