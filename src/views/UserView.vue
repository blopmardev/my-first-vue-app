<template>
  <article v-if="!isLoading">
    <h1>Perfil de {{ user.name }}</h1>
    <section>
      <CustomCard class="user" :key="user.id" :user="user.name">
        <template v-slot:header>
          <h2>{{ user.name }}</h2>
        </template>
        <template v-slot:picture v-if="user.avatar">
          <img :src="user.avatar" alt="Avatar del usuario" title="Avatar del usuario" class="avatar">
        </template>
        <template v-slot:picture v-else>
          <img src="../assets/logo.png" alt="Avatar del usuario" title="Avatar del usuario" class="avatar">
        </template>
        <template v-slot:footer>
          <h3>Id de Usuario: {{ user.id }}</h3>
          <h3>E-mail: {{ user.email }}</h3>
          <h3>Rol de usuario: {{ user.role }}</h3>
          <h3>Se unió a FakEcommerce: {{ user.creationAt }}</h3>
          <CustomButton @click="addElementToCart(user)">
            <template v-slot:text>Añadir al 🛒</template>
          </CustomButton>
        </template>
      </CustomCard>
    </section>
  </article>
  <article v-else>
    <h2>Cargando...</h2>
  </article>
</template>

<script lang="ts">
import { useCart } from '@/composables/useCart'
import useUsers from '@/composables/useUsers';
import { defineComponent} from 'vue';
import CustomCard from '../components/CustomCard.vue';
import CustomButton from '../components/CustomButton.vue';

export default defineComponent({
  name: 'UserComponent',
  components: {
    CustomCard,
    CustomButton
  },

  props: {
    id: {
      type: Number,
      required: true,
    },
    userRole: String
  },

  setup(props) {
    const { addElementToCart } = useCart();
    const { user, fetchUserById, isLoading } = useUsers();
    fetchUserById(props.id);
    return {
      user,
      addElementToCart,
      isLoading
    };
  },
});
</script>

<style scoped>
.user {
  background-color: #539678;
  width: 70%;
}

h2 {
  color: #ffffff;
}

button {
  width: 50%;
  height: 25%;
  font-size: larger;
  background-color: #2c3e50;
}
</style>