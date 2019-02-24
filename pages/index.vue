<template>
  <section>
    <h1 class="header">Nuxt TypeScript Starter</h1>
    <div>
      <UserList :people="people"></UserList>
    </div>
  </section>
</template>

<script lang="ts">
import { Component, Vue } from "nuxt-property-decorator";
import { State } from "vuex-class";
import { Person } from "~/types";
import UserList from "~/components/UserList.vue";

@Component({
  components: {
    UserList
  }
})
export default class extends Vue {
  @State people: Person;
}
</script>

<style scoped>
</style>
