<template>
    <div class="about-page">
      <h1 class="title">About Us</h1>
      <p>This is the About page where you can find information about this application.</p>
      <div class="quote-container">
        <p v-for="(letter, index) in motivationalQuote" :key="index" class="quote-letter">{{ letter }}</p>
      </div>
      <div class="social-links">
        <a href="https://www.instagram.com/gill_hyrss?igsh=MWh1ZzMxZTYzN2p0MA==" target="_blank" @click="animateIcon($event)">
          <img src="https://upload.wikimedia.org/wikipedia/commons/a/a5/Instagram_icon.png" alt="Instagram" class="social-icon" />
        </a>
        <a href="https://github.com/GilangHyrs" target="_blank" @click="animateIcon($event)">
          <img src="https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png" alt="GitHub" class="social-icon" />
        </a>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'AboutPage',
    data() {
      return {
        motivationalQuote: 'Keep pushing your limits, and the only limit you will have is the one you set yourself.'.split('')
      };
    },
    mounted() {
      this.animateQuote();
    },
    methods: {
      animateQuote() {
        const letters = document.querySelectorAll('.quote-letter');
        letters.forEach((letter, index) => {
          setTimeout(() => {
            letter.classList.add('show');
          }, index * 100);
        });
      },
      animateIcon(event) {
        const icon = event.currentTarget.querySelector('.social-icon');
        icon.classList.add('clicked');
        setTimeout(() => {
          icon.classList.remove('clicked');
        }, 500); 
      }
    }
  };
  </script>
  
  <style>
  .about-page {
    text-align: center;
    padding: 20px;
    position: relative;
    overflow: hidden;
  }
  
  .about-page .title {
    font-size: 2.5em;
    margin-bottom: 20px;
    font-weight: bold;
    font-family: 'Playfair Display', serif; 
    color: #0b0b0b;
  }
  
  .about-page p {
    font-size: 1.2em;
    color: #000000;
    font-weight: bold;
  }
  
  .quote-container {
    display: inline-block;
    margin-top: 20px;
  }
  
  .quote-letter {
    display: inline-block;
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.5s ease, transform 0.5s ease; 
    margin-right: 5px;
  }
  
  .quote-letter.show {
    opacity: 1;
    transform: translateY(0);
  }
  
  .social-links {
    margin-top: 20px;
  }
  
  .social-icon {
    width: 40px;
    height: 40px;
    margin: 0 10px;
    transition: transform 0.5s ease;
  }
  
  .social-icon.clicked {
    transform: scale(1.2);
  }
  </style>
  