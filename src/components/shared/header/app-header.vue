<template>
  <header>
    <div class="limit">
      <router-link to="/" class="logo">
        <img src="@/assets/logo.png" alt="">
      </router-link>
      <navigation :nav="nav"/>
      <div class="cont">
        <a
            v-for="item in this.mailFiltered"
            :href="'mailto:'+item.value"
        >
          <app-icon :svg="'envelope'"/>
          {{ item.text }}
        </a>

        <span
            v-for="item in this.locationFiltered"
        >
          <app-icon :svg="'pin'"/>
          {{ item.text }}
        </span>
      </div>

      <div class="user-block">
        <app-icon :svg="'user'"/>
        <div class="user-name" v-if="auth">
          {{ userName }}
        </div>
        <div class="favorite">
          <app-icon :svg="'favorite'"/>
          <span v-if="inFavorite > 0 || inFavorite==='9+'">{{ this.inFavoriteF }}</span>
        </div>
        <div class="cart">
          <app-icon :svg="'cart'"/>
          <span v-if="inBasket > 0 > 0 || inBasket==='9+'">{{ this.inBasketF }}</span>
        </div>
      </div>
    </div>
    <div class="bottom-side">
      <div class="limit">
        <div class="catalog-button">
          <app-icon :svg="'catalog'"/>&nbsp;Каталог товарів
        </div>
        <div class="search">
          <input type="text" placeholder="Поиск ...">
          <div class="icon">
            <app-icon :svg="'search'"/>
          </div>
        </div>
        <div class="soc">
            <a
                v-for="item in this.socialFiltered"
                :href="item.val"
                target="_blank"
            >
              <app-icon :svg="item.text"/>
            </a>
        </div>
        <div class="graph">
          <app-icon :svg="'clock'"/>
          Пн-Пт: &nbsp; {{ workingHours.weekdays }}
          <span>|</span>
          Сб-Вс: &nbsp; {{ workingHours.weekends }}
        </div>
        <div class="phone">
          <app-icon :svg="'phone'"/>
          <div class="phone-container">
            <a v-for="item in this.phoneFiltered"
                :href="'tel:'+item.val"
            >
              {{ item.text }}
            </a>
          </div>
          <div class="arrow" v-if="this.phoneFiltered.length > 1">
            <app-icon :svg="'arrow-down'"/>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<script>

import Navigation from "@/components/shared/navigation";
import AppIcon from "@/components/shared/ui/app-icon";

export default {
  name: "app-header",
  components: {AppIcon, Navigation},
  props: ["nav", "contacts", "workingHours"],
  data() {
    return {
      auth: true,
      inFavorite: 2,
      inBasket : 35,
      userName: 'Максименко Олегович'
    }
  },
  computed: {
    phoneFiltered(){
      let vm = this;
      return vm.contacts.filter(contact => {
        return contact.type === 'phone'
      })
    },
    mailFiltered(){
      let vm = this;
      return vm.contacts.filter(contact => {
        return contact.type === 'email'
      })
    },
    locationFiltered(){
      let vm = this;
      return vm.contacts.filter(contact => {
        return contact.type === 'location'
      })
    },
    socialFiltered(){
      let vm = this;
      return vm.contacts.filter(contact => {
        return contact.type === 'social'
      })
    },
    inFavoriteF() {
      let out='';
      if (this.inFavorite >= 10) {
        out = '9+'
      }
      else {
        out = this.inFavorite
      }
      return out
    },
    inBasketF() {
      let out='';
      if (this.inBasket >= 10) {
        out = '9+'
      }
      else {
        out = this.inBasket
      }
      return out
    }
  }
}
</script>

<style scoped lang="scss">
@import "app-header";
</style>