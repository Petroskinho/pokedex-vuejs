<script setup>
import { onMounted, ref } from 'vue';

let vetor = ref([]);
let carregamento = ref(true);
let termo_filtragem = ref('');

onMounted(async () => {

    for(let indice = 1; indice <= 151; indice++){
        let req = await fetch(`https://pokeapi.co/api/v2/pokemon/${indice}`);
        let pokemon = await req.json();

        vetor.value.push(pokemon);
    }

    carregamento.value = false;
});

function filtrar(){
    return vetor.value.filter(obj =>
        obj.name.includes(termo_filtragem.value.toLowerCase())
    );
}
</script>

<template>

    <div class="carregamento" v-if="carregamento">
        <img src="../complementos/carregamento.gif" alt="">
    </div>

    <main class="row" v-else>

        <div class="row">
            <div class="col-12">
                <input
                    type="text"
                    v-model="termo_filtragem"
                    placeholder="Qual pokemon gostaria de procurar?"
                    class="form-control pesquisa"
                >
                <p v-if="filtrar().length == 0">Não foi encontrado nenhum pokemon.</p>
                <p v-else-if="filtrar().length == 1">Foi encontrado um pokemon</p>
                <p v-else>Foram encontrados {{ filtrar().length }} pokemons</p>
            </div>
        </div>

        <div
            class="col-12 col-sm-6 col-md-4 col-lg-3"
            v-for="v in filtrar()"
            :key="v.id"
        >
            <div class="card" :class="v.types[0].type.name">

                <img
                    :src="v.sprites.other.home.front_default"
                    alt=""
                >

                <p>{{ v.name }}</p>

            </div>
        </div>

    </main>

</template>