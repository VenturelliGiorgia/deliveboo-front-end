<template>
  <header class="navbar bg-light fixed-top navbar-expand-lg shadow" id="navbar">
    <div class="container">
      <router-link class="navbar-brand d-flex align-items-center" :to="'/'" @click="onLogoClick()">
        <div class="logo fs-2 fw-bold d-flex align-items-center custom-color" style="height: 48px">
          <i class="fa-solid fa-bowl-food px-2"></i>
          DeliveBoo
        </div>
      </router-link>
      <button class="navbar-toggler" type="button" data-bs-toggle="offcanvas" data-bs-target="#offcanvasNavbar"
        aria-controls="offcanvasNavbar">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="offcanvas offcanvas-end" tabindex="-1" id="offcanvasNavbar" aria-labelledby="offcanvasNavbarLabel">
        <div class="offcanvas-header">
          <div class="offcanvas-title" id="offcanvasNavbarLabel">
            <div class="logo fs-2 fw-bold d-flex align-items-center custom-color" style="height: 48px">
              <i class="fa-solid fa-bowl-food px-2"></i>
              DeliveBoo
            </div>
          </div>
          <button type="button" class="btn-close" data-bs-dismiss="offcanvas" aria-label="Close"></button>
        </div>
        <div class="offcanvas-body">
          <ul class="navbar-nav justify-content-end flex-grow-1 pe-3">
            <li class="nav-item" v-for="element, i in store.dt.arr.headerLinks">
              <a v-if="element.url === 'http://127.0.0.1:8000'" class="nav-link" :class="element.active ? 'active' : ''"
                @click="onLinkClick(element)" :href="element.url"><i :class="element.icon" class="me-2 ms-2"></i>{{
                  element.name }}</a>
              <router-link v-else class="nav-link"
                :class="(element.active ? 'active' : '') + (store.dt.arr.myChart.length > 0 && i === 2 ? ' custom-color' : '')"
                @click="onLinkClick(element)" :to="element.url"><i :class="element.icon" class="me-2 ms-2"></i>{{
                  element.name }}
                <span v-if="i === 2 && store.dt.arr.myChart.length > 0">( {{ quantity }} )</span>
              </router-link>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </header>
  <div class="header-spacer"></div>
</template>

<script>
import { store } from "../stores/main-store";

export default {
  data() {
    return {
      store,

    };
  },
  methods: {
    onLinkClick(obj) {
      store.dt.arr.selectedCategories = [];
      store.dt.arr.headerLinks.forEach((element) => {
        element.active = false;
      });
      obj.active = true;
    },
    onLogoClick() {
      store.dt.arr.selectedCategories = [];
      store.dt.arr.headerLinks.forEach((element) => {
        element.active = false;
      });
    }
  },

  computed: {
    quantity() {
      let toReturn = 0;
      if (Array.isArray(store.dt.arr.myChart)) {
        store.dt.arr.myChart.forEach(element => {
          toReturn += element.quantity;
        })
      }
      return toReturn;
    }
  },
};


</script>

<style lang="scss" scoped>

.header-spacer {
  height: 74px;
}
</style>
