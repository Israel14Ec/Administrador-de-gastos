<template>
    <form
        class="presupuesto"
        @submit.prevent="definirPresupuesto"
    >

        <Alerta
            v-if="error"
        >
            {{ error  }}
        </Alerta>

        <div class="campo">
            <label for="nuevo-presupuesto">Definir Presupuesto</label>
            <input 
                type="number"
                id="nuevo-presupuesto"
                class="nuevo-presupuesto"
                placeholder="Añade tu presupuesto"
                min="0"
                v-model.number="presupuesto"
            >
        </div>

        <input type="submit" value="Definir Presupuesto">
    </form>
</template>

<script setup>

    import { ref} from 'vue'
    import Alerta from './Alerta.vue'

    const presupuesto = ref(0)
    const error = ref('')

    const emit = defineEmits(['definir-presupuesto'])

    const definirPresupuesto = () => {
        if(presupuesto.value <= 0 || presupuesto.value == ""){
            error.value = "Presupuesto no valido"
            
            setTimeout(() => {
                error.value = ''
            }, 4000);
            return
        }
        
        emit('definir-presupuesto', presupuesto.value)
    }

</script>

<style scoped>

    .presupuesto {
        width: 100%;
    }
    
    .campo {
        display: grid;
        gap: 2rem;
    }

    .presupuesto label {
        font-size: 2rem;
        margin-bottom: 2rem;
        text-align: center;
        color: var(--azul);
        text-transform: uppercase;
        font-weight: 600;
    }
    .presupuesto input[type="number"]{
        background-color: var(--gris-claro);
        border-radius: 1rem;
        padding: 1rem;
        border: none;
        font-size: 2rem;
        text-align: center;
    }

    .presupuesto input[type="submit"]{
        background-color: var(--azul);
        border: none;
        padding: 1rem;
        text-align: center;
        font-size: 1.5rem;
        margin-top: 2rem;
        color: var(--blanco);
        font-weight: 900;
        width: 100%;
        display: flex;
        justify-content: center;
        transition: background-color 300ms ease;

        @media(min-width: 768px) {
            display: block;
            margin: 2rem auto;
            width: 80%;
        }   
    }

    .presupuesto input[type="submit"]:hover{
        background-color: #1048A4;
        cursor: pointer;
    }
    
</style>