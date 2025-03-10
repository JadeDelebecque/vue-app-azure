<template>
  <!-- Conteneur principal de l'affichage du calcul -->
  <div class="calcul-container">
      <div class="ecran">
          {{ affichageCalcul }}
          <span v-if="props.result === 1"> = </span>
      </div>
      <div class="ecran resultat">
          <span v-if="props.result === 1">{{ realiserCalcul }}</span>
      </div>
  </div>
</template>

<script setup>
import { computed } from 'vue';

// Définition des props pour recevoir les valeurs des opérateurs et de l'opération
const props = defineProps({
  leftOperator: {
      type: [Number, String],
      required: true,
      default: ""
  },
  operation: {
      type: String,
      required: true,
      default: ' '
  },
  rightOperator: {
      type: [Number, String],
      required: true,
      default: ""
  },
  result: Number // Indique si l'on doit afficher le résultat
});

// Calcul du résultat en fonction de l'opération
const realiserCalcul = computed(() => {
  if (props.result === 1) {
      switch (props.operation) {
          case '+':
              return props.leftOperator + props.rightOperator;
          case '-':
              return props.leftOperator - props.rightOperator;
          case '*':
              return props.leftOperator * props.rightOperator;
          case '/':
              return props.rightOperator !== 0 ? props.leftOperator / props.rightOperator : 'Erreur';
          default:
              return 0;
      }
  }
  return '';
});

// Génération de l'affichage du calcul sous forme de texte
const affichageCalcul = computed(() => {
  return `${props.leftOperator} ${props.operation} ${props.rightOperator}`;
});
</script>

<style scoped>
/* Conteneur principal */
.calcul-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  max-width: 300px;
  margin: auto;
  padding: 10px;
  border: 2px solid #333;
  border-radius: 10px;
  background-color: #f8f9fa;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
}

/* Style de l'écran */
.ecran {
  background-color: #fff;
  padding: 15px;
  text-align: right;
  font-size: 1.8rem;
  font-family: 'Courier New', Courier, monospace;
  border-radius: 5px;
  margin-bottom: 10px;
  min-height: 3rem;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.1);
  width: 100%;
  color: #333;
}

/* Spécifique à l'affichage du résultat */
.resultat {
  font-weight: bold;
  color: #007bff;
}
</style>
