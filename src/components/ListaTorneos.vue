<template>
  <div>
    <h1>Lista de Torneos</h1>
    <button @click="obtenerTorneos">Cargar Torneos</button>
    <ul v-if="torneos.length">
      <li v-for="torneo in torneos" :key="torneo.id">
        🏆 {{ torneo.nombre }} - {{ torneo.categoria }}
      </li>
    </ul>
    <p v-else>No hay torneos disponibles</p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "ListaTorneos",  //  Nombre del componente corregido
  data() {
    return {
      torneos: []
    };
  },
  methods: {
    async obtenerTorneos() {
      const username = "admin";  
      const password = "admin";  
      const credentials = btoa(`${username}:${password}`);

      try {
        const response = await axios.get("https://mohbenbou.pythonanywhere.com/api/v1/torneos/", {
          headers: {
            Authorization: `Basic ${credentials}`,  
            "Content-Type": "application/json"
          }
        });
        this.torneos = response.data;
      } catch (error) {
        console.error("❌ Error al obtener torneos:", error);
        alert("Error al obtener torneos. Revisa la consola.");
      }
    }
  }
};
</script>
