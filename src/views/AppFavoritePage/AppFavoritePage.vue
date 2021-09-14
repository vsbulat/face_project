<template>
<div class="favorite">
  <div class="limit">
    <template v-if="$store.state.inFavorite>0">
      <div class="h1">Обране</div>
      <app-sorting-block :sorting="sorting"></app-sorting-block>
      <div class="favorite-container">
      </div>
    </template>
    <div class="favorite-empty" v-else>
      <div class="h2">Обраних товарів нема</div>
    </div>

  </div>
</div>
</template>

<script>
import AppCard from "@/components/shared/card/app-card";
import AppSortingBlock from "@/components/shared/app-sorting-block";
export default {
  name: "AppFavoritePage",
  components: {AppSortingBlock, AppCard},
  data() {
    return {
      sorting: [
        'Від дешевих до дорогих',
        'Від дорогих до  дешевих'
      ],
    }
  }
}
</script>

<style scoped lang="scss">
.favorite-container {
  display: grid;
  grid-template-columns: repeat(5 , 1fr);
}
.favorite-empty {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>