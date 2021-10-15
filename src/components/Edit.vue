<template>
    <div class="form" >
        <h1 class="form__title">Actualizar Cancha</h1>
        <label >
        <v-form ref="form" lazy-validation @submit.prevent="actualizarCancha(canchaActualizar)">
            <v-text-field
            v-model="canchaActualizar.complejoDeportivo"
            label="Nombre del complejo deportivo"
            :counter="50"
            ></v-text-field>

            <v-text-field
            v-model="canchaActualizar.numCancha"
            label="Número de la cancha"
            type="number"
            ></v-text-field>

            <v-select
            v-model="canchaActualizar.disponibilidad"
            :items="items"
            label="Disponibilidad"
            ></v-select>

            <v-text-field
            v-model="canchaActualizar.phFds"
            label="Precio fines de semana"
            type="number"
            ></v-text-field>

            <v-text-field
            v-model="canchaActualizar.phEs"
            label="Precio entre semana"
            type="number"
            ></v-text-field>
            <v-btn color="success" class="mr-4" @click="actualizar">
                Guardar
            </v-btn>
        </v-form>
        </label>
    </div>
</template>

<script>
import store from "../store/index.js";
export default {

    data: () => {
    return {
        canchaActualizar: {},
        disponibilidad: null,
        items: [
            "Disponible",
            'No disponible',
        ],
    }
    },
    name: 'actualizar',
    methods:{
        atras(){
            //Redirigir a las canchas
            this.$router.push('/home');
        },
        actualizar(){
            if (this.$refs.form.validate()) {
                //Crear una persona; realiza solicitud post al backend
                store.dispatch("actualizarCancha", this.canchaActualizar).then(()=>{
                    //Limpia el formulario cuando se registra una persona
                    this.$refs.form.reset();
                });
                alert("Cancha actualizada con éxito")
                this.$router.push('/home');
            }
        },
    },
    mounted(){
        fetch(`http://localhost:3000/canchas/${this.$route.params.id}`)
            .then(res => res.json())
            .then( data => {
                this.canchaActualizar = data
            })
    }
}
</script>

<style>
.form{
    display: flex;
    flex-direction: column;
    padding: 20px 30px 20px 30px;
}

.form__title{
    text-align: center;
}
</style>