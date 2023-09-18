<template>
    <div>
      <h1>Canciones</h1>
      <ul>
        <li v-for="song in songs" :key="song.id">
          {{ song.title }} <span>&#8226;</span> {{ song.artist }} <span>&#8226;</span> {{ song.album }}
          <button @click="editSong(song)">Editar</button> <span></span>
          <button @click="deleteSong(song.id)">Eliminar</button>
        </li>
      </ul>
      <div>
        <button @click="addSong">Agregar Canción</button>
        <div v-if="isAdding">
          <input v-model="newSong.title" placeholder="Título de la canción" />
          <input v-model="newSong.artist" placeholder="Artista de la canción" />
          <input v-model="newSong.album" placeholder="Álbum de la canción" />
          <button @click="saveSong">Guardar</button>
        </div>
      </div>
  
    
      <div v-if="isEditing">
        <h2>Editar Canción</h2>
        <input v-model="editedSong.title" placeholder="Nuevo título" />
        <input v-model="editedSong.artist" placeholder="Nuevo artista" />
        <input v-model="editedSong.album" placeholder="Nuevo álbum" />
        <button @click="updateSong">Actualizar</button>
        <button @click="cancelEdit">Cancelar</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        songs: [
          { id: 1, title: "Down Under", artist: "Men At Work", album: "Business as Usual" },
          { id: 2, title: "Don't Let Me Down", artist: "The Beatles", album: "Let it Be" },
          { id: 3, title: "Bed Of Roses", artist: "Bon Jovi", album: "Keep The Faith" },
        ],
        isAdding: false,
        isEditing: false,
        newSong: {
          title: "",
          artist: "",
          album: "",
        },
        editedSong: {
          id: null,
          title: "",
          artist: "",
          album: "",
        },
      };
    },
    methods: {
      addSong() {
        this.isAdding = true;
      },
      saveSong() {
        // Genera un nuevo ID para la canción
        const newId = Math.max(...this.songs.map(song => song.id), 0) + 1;
        this.songs.push({
          id: newId,
          title: this.newSong.title,
          artist: this.newSong.artist,
          album: this.newSong.album,
        });
        this.isAdding = false;
        this.newSong.title = "";
        this.newSong.artist = "";
        this.newSong.album = "";
      },
      editSong(song) {
        // Abre el cuadro de diálogo de edición y muestra los detalles de la canción a editar
        this.isEditing = true;
        this.editedSong.id = song.id;
        this.editedSong.title = song.title;
        this.editedSong.artist = song.artist;
        this.editedSong.album = song.album;
      },
      updateSong() {
        // Actualiza los detalles de la canción en la lista
        const index = this.songs.findIndex(song => song.id === this.editedSong.id);
        if (index !== -1) {
          this.songs[index].title = this.editedSong.title;
          this.songs[index].artist = this.editedSong.artist;
          this.songs[index].album = this.editedSong.album;
          this.isEditing = false;
          this.editedSong.id = null;
          this.editedSong.title = "";
          this.editedSong.artist = "";
          this.editedSong.album = "";
        }
      },
      cancelEdit() {
        // Cancela la edición y cierra el cuadro de diálogo de edición
        this.isEditing = false;
        this.editedSong.id = null;
        this.editedSong.title = "";
        this.editedSong.artist = "";
        this.editedSong.album = "";
      },
      deleteSong(id) {
        const index = this.songs.findIndex(song => song.id === id);
        if (index !== -1) {
          this.songs.splice(index, 1);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  /* Estilos */
  h1 {
    font-size: 24px;
    color: #1db954;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    margin: 10px 0;
  }
  
  button {
    background-color: #1db954;
    color: white;
    border: none;
    padding: 5px 10px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #1ed760;
  }
  
  /* Estilos para el cuadro de diálogo de edición */
  div[isEditing] {
    background-color: #f1f1f1;
    padding: 10px;
    margin-top: 10px;
    border: 1px solid #ddd;
  }
  </style>
  