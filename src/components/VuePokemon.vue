<template>

    <div id="pokemon">
        



    <div class="card">
            <div class="card-image">
                 <figure>
                    <img :src="currentImg">
                 </figure>
            </div>
        <div class="card-content">
             <div class="media">
                <div class="media-content">
                     <p class="title is-3">{{ numero }} - {{ name[0].toUpperCase() + name.slice(1)}}</p>
                     <p class="title is-5">{{ pokemon.type}}</p>
                </div>
      
            </div>

            <div class="content">
                <button class="button is-medium is-fullwidth" @click="mudarSprit">Mudar Sprit</button>
            </div>
        </div>
    </div>


    </div><!--FIM DIV PAI -->

</template>


<script>

    import axios from 'axios';

    export default{

        created: function(){

            axios.get(this.url)
                .then((res)=>{
                    this.pokemon.type = res.data.types[0].type.name;
                    this.pokemon.front = res.data.sprites.front_default;
                    this.pokemon.back = res.data.sprites.back_default;
                    this.currentImg = this.pokemon.front
                    console.log(res)
                })
                .catch()

        },

        data(){
            return{
                isFront: true,
                currentImg: '',
                pokemon: {
                    type: "",
                    front: "",
                    back: ""

                }
            }
        },

        props:{
            numero: Number,
            name: String,
            url: String
        },

        methods:{

            mudarSprit: function(){
                if(this.isFront){
                    this.isFront = false;
                    this.currentImg = this.pokemon.back;
                }else{
                    this.isFront = true;
                    this.currentImg = this.pokemon.front;
                }
            }

        }

       
    }

    

    
     
   
  

</script>


<style>
#pokemon{
    margin-top: 2%;
}
</style>