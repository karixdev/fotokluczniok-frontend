<template>
  <div id="app">
    <router-view/>
    <Footer />
  </div>
</template>

<script>
import Footer from './components/Footer.vue';

export default {
  name: 'App',
  components: {
    Footer,
  },
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Inconsolata&display=swap');
@import './assets/icofont.css';

* {
  font-family: 'Inconsolata', monospace;
}

.custom-form {
  input, select, textarea {
    border: 1px solid #000000;
    color: #000000;
    border-radius: 0;
    outline: none !important;
    resize: none;
  }

  .custom-file {
    label {
      border: 1px solid #000;
      border-radius: 0;
    }
  }

  .btn {
    border: 1px solid #000000;
    color: #000000;
    border-radius: 0;
    outline: none !important;

    &:hover {
      border: 1px solid #000000;
      background-color: #000000;
      color: #ffffff;
    }

    &:focus {
      outline: none !important;
      box-shadow: none;
    }
  }
}

.form-holder {
  margin: 0 auto;
  margin-top: 50px;
  margin-bottom: 50px;
}

input, label {
  outline: none !important;

  &:focus {
    outline: none !important;
  }
}

.section-header {
  $padding: 12px;
  padding-top: $padding;
  padding-bottom: $padding;
  &:last-child {
    text-align: right;
  }
}

.section-add-btn {
  text-decoration: none;
  color: #000;
  border: 1px solid #000;
  padding: 8px;
  transition: all 0.1s ease-out;

  &:hover {
    text-decoration: none !important;
    color: #fff;
    background: #000;
  }
}

.delete-row {
  color: red;
  text-decoration: underline;
  border: none;
  background: none;

  &:hover {
    color: red;
  }
}

.edit-row {
  color: #FFC107;
  text-decoration: underline;

  &:hover {
    color: #FFC107;
  }
}

.custom-btn {
  margin-bottom: 8px;
  background-color: #fff;
  color: #000;
  border: 1px solid #000;
  border-radius: 0;
  margin-left: 4px;

  &:hover {
    background-color: #000;
    color: #fff;
  }
}

.single-gallery-link {
  color: #000;
  text-decoration: underline;

  &:hover {
    color: #000;
  }
}

.fade-enter-active, .fade-leave-active {
  transition: all 1.5s;
}
.fade-enter, .fade-leave-to {
  transform: translateX(10px);
  opacity: 0;
}

.delete-checkbox-label {
  cursor: pointer;
}

.modal-backdrop
{
    opacity:0.5 !important;
}
</style>
