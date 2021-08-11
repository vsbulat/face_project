<template>
  <div class="nav">
    <ul>
      <li v-for="item in nav">
        <router-link :to="item.link">
          {{ item.txt }}
        </router-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "navigation",
  props:["nav"]
}
</script>

<style scoped lang="scss">
@import "../../style/variables";
.nav {
  ul {
    list-style: none;
    display: flex;

    li {
      margin-right: 50px;

      &:last-of-type {
        margin-right: 0;
      }
    }

    a {
      text-transform: uppercase;
      font-size: 14px;
      color: $white;
      text-decoration: none;
      position: relative;

      &::after {
        content: "";
        width: 0;
        height: 2px;
        position: absolute;
        top: 100%;
        left: 50%;
        transform: translateX(-50%);
        background-color: $main;
        transition: width, 0.25s;
      }

      &:hover {
        &::after {
          width: 100%;
        }
      }
    }
  }

}
</style>