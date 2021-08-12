<template>
 <footer>
   <div class="limit">
     <div class="box">
       <router-link to="/" class="logo">
         <img src="@/assets/logo.png" alt="">
       </router-link>
       <ul>
         <li v-if="this.mailFiltered.length">
           <app-icon :svg="'envelope'"/>
           <a
               v-for="item in this.mailFiltered"
               :href="'mailto:'+item.value"
           >

             {{ item.text }}
           </a>
         </li>
         <li v-if="this.phoneFiltered.length">
          <app-icon :svg="'phone'"/>
<!--              <a v-for="item in this.phoneFiltered"
                :href="'tel:'+item.val"
             >
               {{ item.text }}
             </a>-->
             <a :href="'tel:'+this.phoneFiltered[0].val">
               {{ this.phoneFiltered[0].text }}
             </a>
         </li>
         <li  v-if="this.locationFiltered.length">
           <app-icon :svg="'pin'"/>
           <span
                 v-for="item in this.locationFiltered"
             >
            {{ item.text }}
          </span>
         </li>
         <li>
           <app-icon :svg="'clock'"/>
           Пн-Пт: {{ workingHours.weekdays }} Сб-Вс: {{ workingHours.weekends }}
         </li>
       </ul>
       <div
           class="soc-container"
           v-if="this.socialFiltered.length"
       >
         <a
             v-for="item in this.socialFiltered"
             :href="item.val"
             target="_blank"
         >
           <app-icon :svg="item.text"/>
         </a>
       </div>
     </div>

     <div class="box catalog-box">
     <div class="heading" v-if="footerNav.length">Категорії</div>
       <ul v-if="footerNav.length">
         <li v-for="item in footerNav">
           <router-link :to="item.link">
             {{ item.txt }}
           </router-link>
         </li>
       </ul>
     </div>
     <div class="box store">
       <div class="heading">Магазин</div>
       <ul>
         <li v-for="item in navigate">
           <router-link :to="item.link">
             {{ item.txt }}
           </router-link>
         </li>
         <li>
           <router-link to="">Публичная оферта</router-link>
         </li>
         <li>
           <router-link to="">Политика конфиденциальности </router-link>
         </li>
       </ul>
     </div>

     <a
         href="#"
         class="studio"
         v-on:mouseover = "mouseOver"
         v-on:mouseleave = "mouseLive"
     >
       <img :src="require('@/assets/' + logo[active ? 1 : 0])" alt="">
     </a>

   </div>
   <div class="copyright-block">
     <div class="limit">
       <div class="copyright">
         Copyright © {{ new Date().getFullYear() }} . FACE
       </div>
       <div class="right">
         <img src="@/assets/img/liqpay.png" alt="">
         <img src="@/assets/img/visa.png" alt="">
         <img src="@/assets/img/mc.png" alt="">
       </div>
     </div>
   </div>
 </footer>
</template>

<script>
export default {
  name: "app-footer",
  props: ["nav", "contacts", "workingHours", "footerNav"],

  data() {
    return {
      logo: [
          'studio_1.png',
          'studio_2.png'
      ],
      active: false,
      navigate: []
    }
  },

  computed: {
    phoneFiltered() {
      let vm = this;
      return vm.contacts.filter(contact => {
        return contact.type === 'phone'
      })
    },
    mailFiltered() {
      let vm = this;
      return vm.contacts.filter(contact => {
        return contact.type === 'email'
      })
    },
    locationFiltered() {
      let vm = this;
      return vm.contacts.filter(contact => {
        return contact.type === 'location'
      })
    },
    socialFiltered() {
      let vm = this;
      return vm.contacts.filter(contact => {
        return contact.type === 'social'
      })
    },
    navFiltered() {
      let vm = this;
      return vm.nav.filter(n => {
        return n.txt === 'Про нас' || n.txt === 'Оплата і доставка'
      })
    }
  },

  methods: {
    mouseOver() {
      this.active = true;
    },
    mouseLive() {
      this.active = false;
    }
  },

  updated() {
    this.navigate = this.navFiltered;
    //console.log(this.footerNav.length);
  }
}
</script>

<style scoped lang="scss">
  @import "app-footer";
</style>