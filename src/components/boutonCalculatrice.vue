<template>
  <!-- Bouton qui déclenche un événement au clic -->
  <button class="bouton" @click="handleClick">
      {{ value }}
  </button>
</template>

<script setup>
const props = defineProps({
  value: {
      type: [Number, String], 
      required: true
  }
})

const emit = defineEmits(['send-value']); 

// Fonction déclenchée au clic sur le bouton
const handleClick = () => {
  emit('send-value', props.value); 
};
</script>

<style scoped>
/* Style du bouton avec une apparence plus moderne */
.bouton {
  font-size: 1.5rem;
  padding: 12px 20px;
  margin: 5px;
  cursor: pointer;
  background-color: #3498db; 
  color: white; 
  border: none;
  border-radius: 8px; 
}

/* Effet au survol */
.bouton:hover {
  background-color: #2980b9;
}

/* Effet au clic */
.bouton:active {
  background-color: #1c6ea4;
}
</style>
