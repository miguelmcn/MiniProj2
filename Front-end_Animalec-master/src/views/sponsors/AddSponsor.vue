<template>
  <!-- Portfolio Section -->
  <section class="page-section">
    <b-container>
      <HeaderPage title="Adicionar Patrocinador" />

      <!--FORM-->
      <b-row>
        <b-col cols="2"></b-col>
        <b-col>
          <form @submit.prevent="add">
            <div class="form-group">
              <input
                v-model="sponsor.name"
                type="text"
                class="form-control form-control-lg"
                id="txtName"
                placeholder="escreve nome"
                required
              />
            </div>
            <div class="form-group">
              <input
                v-model="sponsor.email"
                type="text"
                class="form-control form-control-lg"
                id="txtEmail"
                placeholder="escreve email"
                required
              />
            </div>
            <div class="form-group">
              <input
                v-model="sponsor.budget"
                type="text"
                class="form-control form-control-lg"
                id="txtBudget"
                placeholder="escreve investimento"
                required
              />
            </div>
            <div class="form-group">
              <select id="sltGroup" class="form-control form-control-lg" v-model="sponsor.animais" required>
                <option value>-- SELECIONA ANIMAIS --</option>
                <option value="trigre">Tigre</option>
                <option value="leão">Leão</option>
                <option value="urso">Urso</option>
                <option value="touro">Touro</option>
              </select>
            </div>
            <button type="submit" class="btn btn-outline-success btn-lg mr-2">
              <i class="fas fa-plus-square"></i>  ADICIONAR</button>
            <router-link
              :to="{name: 'listSponsors'}"
              tag="button"
              class="btn btn-outline-danger btn-lg"
            ><i class="fas fa-window-close"></i>  CANCELAR</router-link>
          </form>
        </b-col>
        <b-col cols="2"></b-col>
      </b-row>
    </b-container>
  </section>
</template>

<script>
import { ADD_SPONSOR } from "@/store/sponsors/sponsor.constants";
import HeaderPage from "@/components/HeaderPage.vue";
import router from "@/router";
import { mapGetters } from "vuex";

export default {
  name: "AddSponsor",
  components: {
    HeaderPage
  },
  data: () => {
    return {
      name: "",
      email: "",
      budget: "",
      animals: [
        ""
      ]
    };
  },
  computed: {
    ...mapGetters("sponsor", ["getMessage"])
  },
  methods: {
    add() {
      this.$store.dispatch(`sponsor/${ADD_SPONSOR}`, this.$data).then(
        () => {
          this.$alert(this.getMessage, "Patrocinador adicionado!", "success");
          router.push({ name: "listSponsors" });
        },
        err => {
          this.$alert(`${err.message}`, "Erro", "error");
        }
      );
    }
  }
};
</script>
