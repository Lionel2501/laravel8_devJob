<template>
    <div>
        <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full"
        :class="claseEstadoVacante()"
        @click="cambiarEstado"
        :key="estadoVacanteData">
            {{ estadoVacante }}
        </span>
    </div>
</template>

<script>
export default {
    props: ['estado', 'vacanteId'],
    mounted() {
        this.estadoVacanteData = Number(this.estado)
    },
    data: function (){
        return{
            estadoVacanteData: null
        }
    },
    methods: {
        cambiarEstado(){
            if(this.estadoVacanteData === 1){
                this.estadoVacanteData = 0;
            } else{
                this.estadoVacanteData = 1;
            }

            const params = {
                estado: this.estadoVacanteData
            }
            //enviar peticion a Axios
            axios.post('/vacantes/' + this.vacanteId, params)
        },
        claseEstadoVacante(){
            return this.estadoVacanteData === 1 ? "bg-green-100 text-green-800" :
            "bg-red-100 text-red-800"
        }
    },
    computed: {
        estadoVacante(){
            return this.estadoVacanteData === 1 ? 'Activa' : 'Inactiva'
        }
    }
}
</script>
