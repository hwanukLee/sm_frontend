<template>
  <div>

    <v-dialog
      v-model="loading"
      hide-overlay
      persistent
      width="300"
    >
      <v-card
        color="primary"
        dark
      >
        <v-card-text>
          Please stand by
          <v-progress-linear
            indeterminate
            color="white"
            class="mb-0"
          ></v-progress-linear>
        </v-card-text>
      </v-card>
    </v-dialog>

    <v-card
      color="indigo"
      class="d-flex mb-2"
      tile
    >
      <v-card-text>
        <v-row>
          <v-col>
            <v-btn
              dark
              text
              class="text-h6 font-weight-black"
            >
              <v-icon>mdi-chevron-right</v-icon>
              <v-label>{{ this.$store.state.category.name }}</v-label>
            </v-btn>
          </v-col>
          <v-col class="ml-auto" sm="12" md="5" lg="3">
            <v-text-field
              v-model="searchTxt"
              label="Search"
              placeholder="코드번호, 주요단어"
              dense
              single-line
              solo
              hide-details
              append-icon="fa-search"
              @click:append="search"
              @keydown.enter="search"
            ></v-text-field>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>

    <section v-if="isCardView">
      <CardContents :items="items" @scrollEnd="loadItems" />
    </section>
    <section v-else>
      <TableContents :items="items" @changePage="loadItems"  @addCart="addCart"/>
    </section>
    
  </div>
</template>
<script>
import CardContents from '@/components/items/card.contents'
import TableContents from '@/components/items/table.contents'

export default {
  components: {
    CardContents,
    TableContents
  },
  name: 'Items',
  data() {
    return {
      searchTxt: '',
      dialog: true
    }
  },
  watch:{
    categoryCode() {
      this.initPage();
    }
  },
  computed: {
    categoryCode() {
      return this.$store.state.category.code;
    },
    items() {
      return this.$store.getters['item/items'];
    },
    loading() {
      return this.$store.getters['item/loading'];
    },
    isCardView() {
      return this.$store.getters['item/isCardView'];
    }
  },
  methods: {
    findAll() {
      this.$store.dispatch('item/findAll', { categoryCode: this.categoryCode });
    },
    search() {
      this.$store.commit('item/resetCount');
      this.$store.commit('item/resetPageNum');
      this.$store.commit('item/resetItems');
      this.$store.dispatch('item/search', { categoryCode: this.categoryCode, searchTxt: this.searchTxt });
    },
    loadItems() {
      this.$store.dispatch('item/searchItems', { categoryCode: this.categoryCode, searchTxt: this.searchTxt });
      setInterval(() => { if (this.$store.getters["item/loading"]) this.$store.commit('item/disableLoading') }, 5000)
    },
    addCart(item) {
      console.log('added Cart', item);
    },
    initPage() {
      this.searchTxt = '';
      this.$store.commit('item/resetCount');
      this.$store.commit('item/resetPageNum');
      this.$store.commit('item/resetItems');
      this.findAll();
    },
    viewChange() {
      this.$store.commit('item/toggleIsCardView');
    }
  },
  mounted() {
    this.initPage();
  }
}
</script>