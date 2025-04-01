<template>
  <div>
    <BanNer />
    <div class="main-container">
      <h1>Monte o seu burguer</h1>
      <BurguerForm />
    </div>
  </div>
</template>

<script>
import BanNer from '@/components/BanNer.vue';
import BurguerForm from '@/components/BurguerForm.vue';

export default {
  name: 'HomeView',
  components: {
    BanNer,
    BurguerForm,
  },
};
</script>
