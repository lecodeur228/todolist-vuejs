

<template>  
    <label for="checkbox">
      <input type="checkbox" id="checkbox" v-model="model" />
      <span>{{ label }}</span>
    </label>
</template>

<script setup>

const model  = defineModel();

// pour definir les proprietes passer en paramètre
const props = defineProps({
     label: String
})

// pour définir les évènements

const emits =  defineEmits(["check", "uncheck"])

const onChange = (e) => {
    if(e.currentTarget.checked){
        emits("check",e.currentTarget)
    } else {
        emits("uncheck",e.currentTarget)
    } 
}



</script>