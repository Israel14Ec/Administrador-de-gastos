<template>
    <div class="dos-columnas">

        <div class="contenedor-grafico">

            <p class="porcentaje"> {{ porcentaje }} %</p>
            <CircleProgress
                :percent="porcentaje"
                :size= "250"
                :border-width="24"
                :border-bg-width="20"
                fill-color="#3B82F6"
                empy-color="#f5f5f5"
            />
        </div>
        
        <div class="contenedor-presupuesto">
            <button
                class="reset-app"
                type="button"
                @click="$emit('reset-app')"
            >
                Resetear App
            </button>

            <p>
                <span>Presupuesto:</span> 
                    {{ formatearCantidad(presupuesto)  }}
            </p>

            <p>
                <span>Disponible:</span> 
                    {{ formatearCantidad(disponible) }}
            </p>
            
            <p>
                <span>Gastado:</span> 
                {{ formatearCantidad(gastado) }} 
            </p>
        </div>

    </div>
</template>

<script setup>
    
    import {computed} from 'vue'
    import {formatearCantidad} from '../helpers'
    import CircleProgress from "vue3-circle-progress";
    import "vue3-circle-progress/dist/circle-progress.css"; 

    defineEmits(['reset-app'])

    const props = defineProps ({
        presupuesto: {
            type: Number,
            required: true
        },
        disponible: {
            type: Number,
            required: true
        },
        gastado: {
            type: Number,
            required: true
        }
    })

    const porcentaje = computed(() => {
        return parseInt((props.gastado / props.presupuesto)*100)  
    })

</script>

<style scoped>

    .contenedor-grafico {
        position: relative;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .porcentaje {
        position: absolute;
        margin: auto;
        top: 40%;
        bottom: 0;
        text-align: center;
        z-index: 100;
        font-size: 3rem;
        font-weight: 900;
        color: var(--gris-oscuro);
    }

    .dos-columnas{
        display: flex;
        flex-direction: column;
    }

    .dos-columnas >:first-child{
        margin-bottom: 3rem;
    }

    @media(min-width: 768px) {
        .dos-columnas{
            flex-direction: row;
            gap: 3rem;
            align-items: center;
        }

            .dos-columnas >:first-child{
            margin-bottom: 0;
        }   
    }

    .contenedor-presupuesto {
        width: 100%;
    }

    .contenedor-presupuesto p {
        font-size: 2rem;
        text-align: center;
        color: var(--gris-oscuro)
    }

    @media(min-width: 768px) {
        .contenedor-presupuesto p {
            font-weight: 900;
            text-align: left;
        }
    }

    .contenedor-presupuesto span {
        font-weight: 700;
        color: var(--azul);
    }

    .reset-app{
        
        background-color: #f60b74;
        border: none;
        padding: 1rem;
        width: 80%;
        color: var(--blanco);
        font-weight: 700;
        text-transform: uppercase;
        border-radius: 1rem;
        transition-property: background-color;
        transition-duration: 300ms;
        
    }

    .reset-app:hover {
        cursor: pointer;
        background-color: #DB2777;
    }

</style>