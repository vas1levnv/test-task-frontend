<template>
  <div class="error" v-if="isError">
    <div>Ошибка!</div>
    {{ error }}
  </div>
  <div class="wrapper">
    <div class="left">
      <div class="top">
        <div class="top-wrapper">
          <Item v-for="item in addedItems" :item="item" :key="item.id"/>
        </div>
      </div>
      <div class="bottom">
        <div class="bottom-wrapper">
          <Item v-for="item in items" @add="addItem" :item="item" :key="item.id"/>
        </div>
      </div>
    </div>
    <div class="right">
      <div class="top">
        <div class="top-wrapper">
          <Item v-for="item in addedSelectedItems" :item="item" :key="item.id"/>
        </div>
      </div>
      <div class="bottom">
        <div class="bottom-wrapper">
          <Item v-for="item in selectedItems" @add="addSelectedItem" :item="item" :key="item.id"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import Item from "@/components/Item.vue";

export default {
  name: 'App',
  components: {Item},
  data() {
    return {
      items: [
        {
          "id": 1,
          "name": "Shoes 1"
        },
        {
          "id": 2,
          "name": "Shoes 2"
        },
        {
          "id": 3,
          "name": "Shoes 3"
        },
        {
          "id": 4,
          "name": "Shoes 4"
        },
        {
          "id": 5,
          "name": "T-shirt 1"
        },
        {
          "id": 6,
          "name": "T-shirt 2"
        },
        {
          "id": 7,
          "name": "T-shirt 3"
        },
        {
          "id": 8,
          "name": "T-shirt 4"
        }
      ],
      addedItems: [],
      isError: false,
      error: '',
      selectedItems: [
        {
          "id": 11,
          "name": "Jacket 1"
        },
        {
          "id": 12,
          "name": "Jacket 2"
        },
        {
          "id": 13,
          "name": "Jacket 3"
        },
        {
          "id": 14,
          "name": "Jacket 4"
        },
        {
          "id": 15,
          "name": "Hoodie 1"
        },
        {
          "id": 16,
          "name": "Hoodie 2"
        },
        {
          "id": 17,
          "name": "Hoodie 3"
        },
        {
          "id": 18,
          "name": "Hoodie 4"
        }
      ],
      addedSelectedItems: [],
    }
  },
  methods: {
    addItem(item) {
      this.isError = false
      if (this.addedItems.length < 6) {
        this.addedItems = [...this.addedItems, item]
        this.addedItems = this.addedItems.reduce((acc, el) => {
          if (acc.includes(el)) {
            this.error = 'вы уже выбрали элемент ' + el.name
            this.isError = true
            return acc;
          }
          return [...acc, el];
        }, []);
      } else {
        this.isError = true
        this.error = 'Нельзя добавлять больше 6 элементов в левую корзину'
      }
    },

    addSelectedItem(item) {
      this.isError = false
      if (this.addedSelectedItems.length < 1) {
        this.addedSelectedItems = [...this.addedSelectedItems, item]
        this.addedSelectedItems = this.addedSelectedItems.reduce((acc, el) => {
          if (acc.includes(el)) {
            this.error = 'вы уже выбрали элемент ' + el.name
            this.isError = true
            return acc;
          }
          return [...acc, el];
        }, []);
      } else {
        this.isError = true
        this.error = 'Нельзя добавлять больше одного элемента в правую корзину'
      }
    },
  }
}
</script>

<style>

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  width: 100vw;
  height: 100vh;
}

.wrapper {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 30px;
  width: 100%;
  height: 100%;
  padding: 15px;
}

.left, .right {
  height: 100%;
  display: flex;
  justify-content: space-between;
  flex-direction: column;
}

.error {
  color: red;
  font-size: 30px;
  font-weight: 900;
  padding: 20px;
  text-align: center;
}

.top {
  border: 5px solid black;
  min-width: 50%;
  padding: 5px;
  min-height: 200px;
  margin-bottom: 30px;
}

.top-wrapper {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

.top .item {
  padding: 5px;
}

.bottom {
  width: 100%;
  flex: 1 1 0;
  border: 5px solid black;
  padding: 20px;
  min-height: 200px;
}

.bottom-wrapper {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
}

.right .top {
  align-self: end;
}

.left .top {
  align-self: start;
}


</style>
