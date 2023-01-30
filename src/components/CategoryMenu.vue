<template>
  <div class="category-menu">
    <h1>Joias&Joias</h1>
    <div class="items">
      <ul>
        <li>
          <p @Click="clickCategoryJoia" @mouseleave="mouseLeave" id="1">Joia</p>
          <p @click="clickCategoryNoivado" @mouseleave="mouseLeave" id="2">Amor e noivado</p>
          <p @click="clickCategoryRelogio" @mouseleave="mouseLeave" id="3">Relógios</p>
          <p @click="clickCategoryMasculinos" @mouseleave="mouseLeave" id="4">Masculinos</p>
          <p @click="clickCategoryPresentes" @mouseleave="mouseLeave" id="5">Presentes</p>
          <p @click="clickCategoryAcessorios" @mouseleave="mouseLeave" id="6">Acessórios</p>
        </li>
      </ul>
    </div>
    <Modal class="Modal" :show="showModal">
      <p v-for="category in categoryJoia" :key="category.title">
        {{category.title}}
      </p>
    </Modal>
    <p></p>

    <!-- <p v-for="category in CategoryInItems" :key="category.title">
        {{ category.title }}
      </p> -->
  </div>
</template>

<script>
import axios from "axios";
import Modal from "./modal.vue";
export default {
  name: "CategoryMenu",
  components: {
    Modal,
  },
  data() {
    return {
      itemsList: [],
      CategoryInItems: [],
      showModal: false,

      categoryJoia: [],
      categoryNoivado: [],
      categoryRelogios: [],
      categoryMasculino: [],
      categoryPresente: [],
      categoryAcessorios: [],
    };
  },
  created() {
    this.getItemsList();
    this.getCategoryModal();
    // this.getCategoryList();
  },
  methods: {
    clickCategoryJoia() {
      this.showModal = true;
    },
    mouseLeave() {
      this.showModal = false;
    },
    getItemsList() {
      this.itemsList = [];
      axios.get("http://localhost:3000/items-menu").then((response) => {
        this.itemsList = response.data;
      });
      console.log(this.itemsList);
    },
    getCategoryModal() {
      this.categoryJoia = [];
      this.categoryNoivado = [];
      this.categoryRelogios = [];
      this.categoryMasculino = [];
      this.categoryPresente = [];
      this.categoryAcessorios = [];
      axios.get("http://localhost:3000/Joia").then((response) => {
        this.categoryJoia = response.data;
      });
      axios.get("http://localhost:3000/Amor-e-Noivado").then((response) => {
        this.categoryNoivado = response.data;
      });
      axios.get("http://localhost:3000/Relogios").then((response) => {
        this.categoryRelogios = response.data;
      });
      axios.get("http://localhost:3000/Masculinos").then((response) => {
        this.categoryMasculino = response.data;
      });
      axios.get("http://localhost:3000/Presentes").then((response) => {
        this.categoryPresente = response.data;
      });
      axios.get("http://localhost:3000/acessorios").then((response) => {
        this.categoryAcessorios = response.data;
      });

      console.log(this.categoryModal);
    },
    // getCategoryList(CategoryItem) {
    //   this.CategoryInItems = [];
    //   let category = CategoryItem || "";
    //   axios.get("http://localhost:3000/" + category).then((response) => {
    //     this.CategoryInItems = response.data;
    //   });
    // },
    expanceMenu() {
      // this.switchCategory(id);
      if (this.showModal == false) {
        // this.comparationIds(id)
        return (this.showModal = true);
      } else {
        return (this.showModal = false);
      }
    },
    // teste(id) {
    //   // console.log("ola")
    //   var ID = id
    //   this.switchCategory(ID);
    // },

    // switchCategory(ID) {
    //   console.log(ID);
    //   var itemId = ID;
    //   var CategoryItem = "/";
    //   // var idItem = 0;
    //   switch (itemId) {
    //     case 1:
    //       CategoryItem = "Joia";
    //       // idItem = 1;
    //       break;
    //     case 2:
    //       CategoryItem = "Amor-e-noivado";
    //       // idItem = 2;
    //       break;
    //     case 3:
    //       CategoryItem = "Relogios";
    //       // idItem = 3;
    //       break;
    //     case 4:
    //       CategoryItem = "Masculinos";
    //       // idItem = 4;
    //       break;
    //     case 5:
    //       CategoryItem = "Presentes";
    //       // idItem = 5;
    //       break;
    //     case 6:
    //       CategoryItem = "Acessorios";
    //     // idItem = 6;
    //   }
    //   console.log(CategoryItem)
    //   this.getCategoryList(CategoryItem);
    //   this.expanceMenu();
    // },
  },
};
</script>

<style lang="less" scoped>
.category-menu {
  height: 20vh;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 20px;
  h1 {
    text-align: center;
    margin: 0;
  }
  .items {
    display: flex;
    justify-content: center;
    ul {
      padding: 0;
      margin: 20px 0 0 0;
      width: calc(100vw - 40vw);
      li {
        list-style: none;
        cursor: pointer;
        display: flex;
        justify-content: space-evenly;
        :hover {
          border-bottom: 2px @blue-green solid;
        }
        p {
          & + p {
            margin-left: 10px;
          }
          margin: 0;
          font-size: 12px;
          .closeMenu {
            height: 12px;
            width: 15px;
            border: none;
          }
        }
      }
    }
  }
}
</style>
