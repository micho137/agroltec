<template>
  <header
    class="header sticky top-0 bg-white shadow-md flex items-center justify-between px-8 py-02"
  >
    <h1 class="w-3/12">
      <a class="flex justify-center items-center" href="">
        <img class="h-16" src="../assets/images/zyro-image.png" alt="logo" />
        <p class="text-xl font-bold">
          AGROL<span class="text-primary">TEC</span> S.A.S.
        </p>
      </a>
    </h1>

    <nav class="nav font-semibold text-lg">
      <ul class="flex items-center">
        <li
          class="p-4 border-b-2 border-primary border-opacity-0 hover:border-opacity-100 hover:text-primary duration-200 cursor-pointer active"
        >
          <a href="/">Inicio</a>
        </li>
        <li
          class="p-4 border-b-2 border-primary border-opacity-0 hover:border-opacity-100 hover:text-primary duration-200 cursor-pointer"
        >
          <a href="/productos">Productos</a>
        </li>
        <li
          class="p-4 border-b-2 border-primary border-opacity-0 hover:border-opacity-100 hover:text-primary duration-200 cursor-pointer"
        >
          <a href="/historial">Historial</a>
        </li>
        <li
          v-if="adminCheck"
          class="p-4 border-b-2 border-primary border-opacity-0 hover:border-opacity-100 hover:text-primary duration-200 cursor-pointer"
        >
          <a href="/adminDashboard">Admin</a>
        </li>
      </ul>
    </nav>

    <div class="w-3/12 flex justify-end">
      <div class="indicator">
        <span
          class="indicator-item badge badge-secondary font-bold cursor-default"
          >{{ store.countCartItems }}</span
        >
        <a href="/carrito">
          <svg
            class="h-8 p-1 hover:text-primary duration-200"
            aria-hidden="true"
            focusable="false"
            data-prefix="far"
            data-icon="shopping-cart"
            role="img"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 576 512"
          >
            <path
              fill="currentColor"
              d="M551.991 64H144.28l-8.726-44.608C133.35 8.128 123.478 0 112 0H12C5.373 0 0 5.373 0 12v24c0 6.627 5.373 12 12 12h80.24l69.594 355.701C150.796 415.201 144 430.802 144 448c0 35.346 28.654 64 64 64s64-28.654 64-64a63.681 63.681 0 0 0-8.583-32h145.167a63.681 63.681 0 0 0-8.583 32c0 35.346 28.654 64 64 64 35.346 0 64-28.654 64-64 0-18.136-7.556-34.496-19.676-46.142l1.035-4.757c3.254-14.96-8.142-29.101-23.452-29.101H203.76l-9.39-48h312.405c11.29 0 21.054-7.869 23.452-18.902l45.216-208C578.695 78.139 567.299 64 551.991 64zM208 472c-13.234 0-24-10.766-24-24s10.766-24 24-24 24 10.766 24 24-10.766 24-24 24zm256 0c-13.234 0-24-10.766-24-24s10.766-24 24-24 24 10.766 24 24-10.766 24-24 24zm23.438-200H184.98l-31.31-160h368.548l-34.78 160z"
              class=""
            ></path>
          </svg>
        </a>
      </div>
      <a @click="cerrarSesion()">
        <label
          class="font-semibold mx-5 text-lg hover:text-primary duration-200 cursor-pointer"
          >Logout</label
        >
      </a>
    </div>
  </header>
</template>

<script>
import { useProductStore } from "../stores/ProductStore";
import { useLoginStore } from "../stores/LoginStore";
export default {
  setup() {
    const store = useProductStore();
    const authStore = useLoginStore();
    return {
      store,
      authStore,
    };
  },
  data: () => {
    return{
      adminCheck: false
    }
  },
  methods: {
    showLogout() {
      this.$swal({
        icon: "success",
        title: "Cerrando sesion, espere unos segundos",
        showConfirmButton: false,
        timer: 1500,
      });
    },
    cerrarSesion() {
      this.authStore.logout(this.showLogout);
    },
    validateAdmin(){
      if (this.authStore.authUser.rol === "ADMIN") {
      this.adminCheck = true
    }
    }
  },
  mounted() {
    this.validateAdmin()
  },
};
</script>
