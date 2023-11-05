<script setup>
import { ref } from "vue";
import { absences, absenceReasons } from "../../data";
import Button from "./Button.vue";
import AbsenceCard from "./AbsenceCard.vue";

const absencesList = ref([]);
const availableIndices = ref([...Array(absences.length).keys()]);

// Funktion för att formatera datum och tid till en läsbar sträng
const formatDateTime = (dateTime) => {
  if (dateTime === null) {
    return "tillsvidare";
  } else if (dateTime) {
    const options = {
      weekday: "long",
      day: "numeric",
      month: "long",
    };
    const timeOptions = {
      hour: "numeric",
      minute: "numeric",
    };
    const date = new Date(dateTime);
    const dateString = date.toLocaleDateString("sv-SE", options);
    const timeString = date.toLocaleTimeString("sv-SE", timeOptions);
    return `${dateString} ${timeString}`;
  }
  return "";
};

// Funktion för att lägga till en slumpmässig frånvaro i frånvarolistan
const addRandomAbsence = () => {
  if (availableIndices.value.length > 0) {
    // Välj en slumpmässig index från tillgängliga index.
    const randomIndex = availableIndices.value.splice(
      Math.floor(Math.random() * availableIndices.value.length),
      1
    )[0];
    const randomPerson = { ...absences[randomIndex], id: randomIndex };
    // Lägg till den slumpmässiga frånvaron i frånvarolistan
    absencesList.value.push(randomPerson);
  }
};

// Funktion för att hämta orsaken till frånvaron baserat på orsakens GUID
const getReason = (reasonGuid) => {
  const matchingReason = absenceReasons.find(
    (reason) => reason.guid === reasonGuid
  );
  return matchingReason ? matchingReason.id : "Okänd orsak"; // Returnera orsaken eller 'okänd orsak' om den inte hittas
};
</script>
  

<template>
  <div>
    <Button :addRandomAbsence="addRandomAbsence">
      +
    </Button>
    <main class="absences-list">
    <AbsenceCard
      v-for="absence in absencesList"
      :key="absence.id"
      :absence="absence"
      :getReason="getReason"
      :formatDateTime="formatDateTime"
    />
    </main>
  </div>
</template>


<style scoped>
main {
  width: 100%; /* bredden till 100% för att fylla hela skärmens bredd */
  display: grid;
  grid-gap: 22px;
  

  @media (max-width: 998px) {
    grid-template-columns: 1fr; /* För skärmar som är mindre än 998px tar varje kort en hel rad */
  }

  @media (min-width: 999px) {
    grid-template-columns: repeat(3, 1fr); /* För skärmar större än 998px, tre kolumner */
  }
}
</style>


  
 