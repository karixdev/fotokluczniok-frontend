<template>
  <div>

    <AdminNav />

    <b-container>
      <b-row>
        <b-col md="12" lg="8" class="content-holder">
          <b-row>
            <b-col lg="3" md="12" class="section-picker-holder">
              <b-list-group>
                <b-list-group-item v-on:click="changeSection(0)" section-id="0">Nagłówki</b-list-group-item>
                <b-list-group-item v-on:click="changeSection(1)" section-id="1">Fotogrfia</b-list-group-item>
                <b-list-group-item v-on:click="changeSection(2)" section-id="2">Galerie</b-list-group-item>
              </b-list-group>
            </b-col>

            <b-col lg="9" md="12">
              <PhotographyGroupTable v-if="getLastId === 0" :items="photographyGroups" />
              <PhotographyTable v-if="getLastId === 1" :items="photographies" />
              <GalleryTable v-if="getLastId === 2" :items="galleries" />
            </b-col>
          </b-row>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import AdminNav from '../components/AdminNav.vue';
import PhotographyGroupTable from '../components/PhotographyGroupTable.vue';
import PhotographyTable from '../components/PhotographyTable.vue';
import GalleryTable from '../components/GalleryTable.vue';

export default {
  name: 'Home',
  components: {
    AdminNav,
    PhotographyGroupTable,
    GalleryTable,
    PhotographyTable,
  },
  data() {
    return {
      photographyGroups: [],
      galleries: [],
      photographies: [],
      displaySpinner: true,
      loaded: false,
    };
  },
  created() {
    this.changeSection(this.$store.getters.getLastSectionId);
  },
  methods: {
    changeSection(id) {
      if (id !== this.$store.getters.getLastSectionId || !this.loaded) {
        const oldId = this.$store.getters.getLastSectionId;

        if (!this.loaded) this.loaded = true;

        this.$store.dispatch('changeLastSectionId', { id })
          .then(() => {
            if (this.getLastId === 0) this.getPhotographyGroups();
            if (this.getLastId === 1) this.getPhotographies();
            if (this.getLastId === 2) this.getGalleries();

            $(`div[section-id='${oldId}']`).removeClass('active');
            $(`div[section-id=${id}]`).addClass('active');
          });
      }
    },
    deleteRow(arr, el) {
      for (let i = 0; i < arr.length; i += 1) {
        if (arr[i].id === el.id) {
          arr.splice(i, 1);
        }
      }
    },
    checkElements(oldArr, newArr) {
      oldArr.forEach((el) => {
        let count = 0;
        newArr.forEach((newEl) => {
          if (newEl.id === el.id) count += 1;
        });

        if (count === 0) this.deleteRow(oldArr, el);
      });
    },
    addNewElementsToArr(oldArr, newArr) {
      newArr.forEach((newEl) => {
        let count = 0;
        oldArr.forEach((el) => {
          if (el.id === newEl.id) count += 1;
        });

        if (count === 0) oldArr.push(newEl);
      });
    },
    getPhotographyGroups() {
      this.$store.dispatch('getPhotographyGroups')
        .then((resp) => {
          this.addNewElementsToArr(this.photographyGroups, resp.data);
          this.checkElements(this.photographyGroups, resp.data);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    getGalleries() {
      this.$store.dispatch('getGalleries')
        .then((resp) => {
          this.addNewElementsToArr(this.galleries, resp.data);
          this.checkElements(this.galleries, resp.data);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    getPhotographies() {
      this.$store.dispatch('getPhotographies')
        .then((resp) => {
          this.addNewElementsToArr(this.photographies, resp.data);
          this.checkElements(this.photographies, resp.data);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
  computed: {
    getLastId() {
      return parseInt(this.$store.getters.getLastSectionId, 10);
    },
  },
};
</script>

<style lang="scss">
.content-holder {
  margin: 0 auto;
  margin-top: 50px;
  margin-bottom: 50px;
}

.section-picker-holder {
  border-right: 1px solid #000;

  @media (max-width: 991px) {
    border-right: none;
    margin-bottom: 16px;
  }

  .list-group-item {
    cursor: pointer;
    border-right: 1px solid #000;
    border-left: 1px solid #000;
    border-top: 1px solid #000;

    &:last-child {
      border-bottom: 1px solid #000;
    }

    transition: all 0.1s ease-out;

    &:hover {
      background-color: #000 !important;
      color: #fff;
      border-color: #000 !important;
      box-shadow: none !important;
    }
  }
}

.active {
  background-color: #000 !important;
  border-color: #000 !important;
  box-shadow: none !important;
}

.custom-table {
  border-top: none !important;
}
</style>
