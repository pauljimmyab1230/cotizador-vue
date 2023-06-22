<script setup>
import { ref, computed } from 'vue';
import Header from './components/Header.vue';
import Button from './components/Button.vue'

const cantidad = ref(10000);
const MAX = 20000;
const MIN = 0;
const STEP = 100;

const formatearDinero = computed(() => {
    const formatter = new Intl.NumberFormat('en-US', {
        style: 'currency',
        currency: 'USD'
    });
    return formatter.format(cantidad.value);
})

const handleChangeDecremento = () => {
    const valor = cantidad.value - STEP;
    if (valor < MIN) {
        alert('La cantidad no es valida');
        return;
    }
    cantidad.value = valor;
}
const handleChangeIncremento = () => {
    const valor = cantidad.value + STEP;
    if (valor > MAX) {
        alert('La cantidad no es valida');
        return;
    }
    cantidad.value = valor;
}

</script>

<template>
    <div class="my-20 max-w-lg mx-auto bg-white shadow p-10 rounded-lg">
        <Header />
        <div class="flex justify-between mt-10">
            <Button :operador="'-'" @fn="handleChangeDecremento" />
            <Button :operador="'+'" @fn="handleChangeIncremento" />

        </div>

        <div class="my-5">
            <input type="range" name="" id="" class="w-full bg-lime-200 accent-lime-500 hover:accent-lime-600" :min="MIN"
                :max="MAX" :step="STEP" v-model.number="cantidad" />
        </div>
        <p class="text-center my-10 text-5xl font-extrabold text-indigo-600">{{ formatearDinero }}</p>
    </div>
</template>
