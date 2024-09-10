<template>
    
    <div id="pokemon">
        <div class="card">
            <div class="card-image">
                <figure>
                <img
                    :src="currentImg" alt="Placeholder image"
                />
                </figure>
            </div>
        <div class="card-content">
                <div class="media">
                

                <div class="media-content">
                    <p class="title is-4">{{num}}-{{ name | upper }}</p>
                    <p class="subtitle is-6">{{ pokemon.type }}</p>
                </div>
                </div>

                <div class="content">
                    <button class="button" @click="mudarSprite">Mudar Sprite</button>
                </div>

  </div>
</div>


    </div>

</template>

<script>
import axios from 'axios';
export default {
    created: function(){ //metodo create serve como uma função chamada no carregamento da pagina
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front;
        })
    },
    data() { //data armazena variaveis
        return {
            isFront: true,
            currentImg: '',
            pokemon: {
                type: '',
                front: '',
                back: ''
            }
        }
    },
    props: { // Props são utilizadas para passar dados entre componentes de Filho para Pai
        name: String,
        url: String,
        num: Number
    },
    filters: { //Filtros são utilizados como logicas para apresentação das informações
        upper: function(value) {
            var newName = value[0].toUpperCase() + value.slice(1);
            return newName;
        }
    },
    methods: { //Metodos onde posso criar funções ou eventos(onclick, onover ETC)
        mudarSprite: function() {
            if (this.isFront) {
                this.isFront = false;
                this.currentImg = this.pokemon.back;
            } else {
                this.isFront = true;
                this.currentImg = this.pokemon.front;
            }
        }
    }
}
</script>

<style scoped>
    #pokemon {
        margin-top: 2%;
    }

    #pokemon p {
        margin-top: 1%;
    }
</style>