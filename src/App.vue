<template>
  <div class="container">

    <!-- GRILLE 4x6 -->
    <div class="grid">
      <div
        v-for="(cell, index) in grid"
        :key="index"
        class="cell"
        @click="selectCell(index)"
      >
        <img v-if="cell !== null" :src="cell" />
      </div>
    </div>

    <!-- MENU CHOIX IMAGE -->
    <div v-if="activeCell !== null" class="panel">
      <h3>Choisir une image</h3>

      <div class="images">
        <img
          v-for="(img, i) in images"
          :key="i"
          :src="img"
          @click="setImage(img)"
        />
      </div>

      <button @click="activeCell = null">Fermer</button>
    </div>

  </div>
</template>

<script>
export default {
  data() {
    const base = import.meta.env.BASE_URL

    return {
      // 24 cases
      grid: Array(24).fill(null),

      // case sélectionnée
      activeCell: null,

      // 12 images
      images: [
        base + "Blop_1.webp",
        base + "Blop_2.jpeg",
        base + "Blop_3.webp",
        base + "Blop_4.jpeg",
        base + "Blop_5.jpeg",
        base + "Blop_6.webp",
        base + "Blop_7.jpeg",
        base + "Blop_8.jpeg",
        base + "Blop_9.webp",
        base + "Blop_10.png",
        base + "Blop_11.webp",
        base + "Blop_12.webp"
      ]
    }
  },

  methods: {
    selectCell(index) {
      this.activeCell = index
    },

    setImage(img) {
      if (this.activeCell === null) return

      this.grid[this.activeCell] = img
      this.activeCell = null
    }
  }
}
</script>

<style>
.container {
  display: flex;
  gap: 40px;
  padding: 20px;
}

/* GRILLE 4x6 */
.grid {
  display: grid;
  grid-template-columns: repeat(6, 100px);
  grid-template-rows: repeat(4, 100px);
  gap: 10px;
}

.cell {
  width: 100px;
  height: 100px;
  background: #444;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  border-radius: 6px;
}

.cell img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* PANEL IMAGE */
.panel {
  width: 220px;
  background: #222;
  color: white;
  padding: 10px;
  border-radius: 10px;
}

.images {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 5px;
}

.images img {
  width: 60px;
  height: 60px;
  cursor: pointer;
  object-fit: cover;
  border: 2px solid transparent;
}

.images img:hover {
  border: 2px solid white;
}
</style>