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
             <a v-for="item in this.phoneFiltered"
                :href="'tel:'+item.val"
             >
               {{ item.text }}
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
           Пн-Пт: &nbsp; {{ workingHours.weekdays }}&nbsp;Сб-Вс: &nbsp; {{ workingHours.weekends }}
         </li>
         <li v-if="this.socialFiltered.length">
           <a
               v-for="item in this.socialFiltered"
               :href="item.val"
               target="_blank"
           >
             <app-icon :svg="item.text"/>
           </a>
         </li>
       </ul>


     </div>

   </div>
 </footer>
</template>

<script>
export default {
  name: "app-footer",
  props: ["nav", "contacts", "workingHours"],

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
    }
  }
}
</script>

<style scoped lang="scss">
  @import "app-footer";
</style>