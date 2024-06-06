<template>
    <div class="modal" v-if="show">
      <div class="modal-content">
        <span class="close" @click="closeModal">&times;</span>
        <div v-if="character">
          <img :src="character.image" :alt="character.name" />
          <h2>{{ character.name }}</h2>
          <p>Status: {{ character.status }}</p>
          <p>Species: {{ character.species }}</p>
          <p>Gender: {{ character.gender }}</p>
          <p>Origin: {{ character.origin.name }}</p>
          <p>Location: {{ character.location.name }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      show: {
        type: Boolean,
        required: true,
      },
      character: {
        type: Object,
        required: true,
      },
    },
    watch: {
      character(newVal) {
        console.log('Character in modal:', newVal);
      }
    },
    methods: {
      closeModal() {
        this.$emit('close');
      },
    },
  };
  </script>
  
  <style scoped>
  .modal {
    display: block; /* Hidden by default */
    position: fixed; /* Stay in place */
    z-index: 1; /* Sit on top */
    left: 0;
    top: 0;
    width: 100%; /* Full width */
    height: 100%; /* Full height */
    overflow: auto; /* Enable scroll if needed */
    background-color: rgba(0,0,0,0.4); /* Black w/ opacity */
  }
  
  .modal-content {
    background-color: #fff; /* White background */
    color: #000; /* Black text color */
    margin: 15% auto; /* 15% from the top and centered */
    padding: 20px;
    border: 1px solid #888;
    width: 80%; /* Could be more or less, depending on screen size */
  }
  
  .close {
    color: #aaa;
    float: right;
    font-size: 28px;
    font-weight: bold;
  }
  
  .close:hover,
  .close:focus {
    color: black;
    text-decoration: none;
    cursor: pointer;
  }
  
  img {
    display: block;
    margin: 0 auto 10px;
  }
  
  h2, p {
    text-align: center;
    margin: 10px 0;
  }
  </style>
  