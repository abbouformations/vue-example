<template>
  <div class="container py-5">
    <div class="card shadow-lg border-0 rounded-4">
      <div class="card-body p-4">
        <h1 class="text-center mb-4 text-primary fw-bold">
          Gestion des Articles
        </h1>

        <!-- Formulaire -->
        <form @submit.prevent="ajouterArticle" class="row g-3 mb-4">
          <div class="col-md-5">
            <input
              v-model="nouvelArticle.nom"
              type="text"
              class="form-control"
              placeholder="Nom de l'article"
              required
            />
          </div>

          <div class="col-md-4">
            <input
              v-model="nouvelArticle.prix"
              type="number"
              class="form-control"
              placeholder="Prix"
              required
            />
          </div>

          <div class="col-md-3 d-grid">
            <button type="submit" class="btn btn-primary">Ajouter</button>
          </div>
        </form>

        <!-- Tableau -->
        <div class="table-responsive">
          <table
            class="table table-bordered table-hover align-middle text-center"
          >
            <thead class="table-dark">
              <tr>
                <th>ID</th>
                <th>Nom</th>
                <th>Prix</th>
                <th>Action</th>
              </tr>
            </thead>

            <tbody>
              <tr v-for="article in articles" :key="article.id">
                <td>{{ article.id }}</td>
                <td>{{ article.nom }}</td>
                <td>{{ article.prix }} €</td>
                <td>
                  <button
                    @click="supprimerArticle(article.id)"
                    class="btn btn-danger btn-sm"
                  >
                    Supprimer
                  </button>
                </td>
              </tr>

              <tr v-if="articles.length === 0">
                <td colspan="4" class="text-muted">Aucun article disponible</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ArticleCrud",

  data() {
    return {
      nouvelArticle: {
        nom: "",
        prix: null,
      },

      articles: [
        { id: 1, nom: "Ordinateur", prix: 1200 },
        { id: 2, nom: "Clavier", prix: 80 },
      ],
    };
  },

  methods: {
    ajouterArticle() {
      const nouvelId =
        this.articles.length > 0
          ? Math.max(...this.articles.map((a) => a.id)) + 1
          : 1;

      this.articles.push({
        id: nouvelId,
        nom: this.nouvelArticle.nom,
        prix: this.nouvelArticle.prix,
      });

      this.nouvelArticle.nom = "";
      this.nouvelArticle.prix = null;
    },

    supprimerArticle(id) {
      this.articles = this.articles.filter((article) => article.id !== id);
    },
  },
};
</script>

<style>
body {
  background: #f8f9fa;
}
</style>
