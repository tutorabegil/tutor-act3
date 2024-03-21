<template>
  <div class="item-list">
    <input type="text" v-model="searchQuery" placeholder="Search items..." class="search-input">
    <div v-for="(item, index) in filteredItems" :key="index" class="item">
      <div class="item-details">
        <div class="item-info">
          <img :src="getImagePath(item.image)" alt="Item Image" class="item-image">
          <div>
            <p class="item-name">{{ item.name }}</p>
            <p class="item-price">Php {{ item.price }}</p>
          </div>
        </div>
      </div>
      <div class="button-group">
        <button @click="addToCart(item)" class="add-to-cart-btn">Add to Cart</button>
        <button @click="updateItem(index)" class="update-btn">Update</button>
        <button @click="removeItem(index)" class="remove-btn">Remove</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: '',
      items: [
        { name: 'Alibaba', price: 10, image: 'alibaba.jpg' },
        { name: 'Boy Bawang', price: 20, image: 'boybawang.jpg' },
        { name: 'Cheez-it', price: 15, image: 'cheezit.jpg' },
        { name: 'Clover', price: 11, image: 'clover.jpg' },
        { name: 'Maruya', price: 32, image: 'maruya.jpg' },
        { name: 'Kobi', price: 23, image: 'kobi.jpg' },
        { name: 'Lumpia', price: 23, image: 'lumpia.jpg' },
        { name: 'Nagaraya', price: 23, image: 'nagaraya.jpg' },
        { name: 'Piattos', price: 23, image: 'piatos.jpg' },
        { name: 'Tomi', price: 23, image: 'tomi.jpg' }
      ]
    };
  },
  computed: {
    filteredItems() {
      return this.items.filter(item =>
        item.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    }
  },
  methods: {
    addToCart(item) {
      this.$emit('add-to-cart', item);
    },
    updateItem(index) {
      const item = this.items[index];
      const newName = prompt('Enter the new name:', item.name);
      const newPrice = parseFloat(prompt('Enter the new price:', item.price));
      
      if (newName && !isNaN(newPrice)) {
        item.name = newName;
        item.price = newPrice;
      }
    },
    removeItem(index) {
      this.items.splice(index, 1);
    },
    getImagePath(image) {
      return `/img/${image}`;
    }
  }
};
</script>

<style scoped>
.item-list {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20px;
}

.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #ccc;
  width: 80%;
}

.item-details {
  flex: 1;
}

.item-info {
  display: flex;
  align-items: center;
}

.item-image {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin-right: 10px;
}

.item-name {
  margin: 0;
  font-weight: bold;
}

.item-price {
  margin: 0;
}

.button-group {
  display: flex;
  gap: 10px;
}

.add-to-cart-btn {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.add-to-cart-btn:hover {
  background-color: #45a049;
}

.update-btn {
  background-color: #fdd835; /* Yellow color */
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.update-btn:hover {
  background-color: #fbc02d; /* Darker yellow color on hover */
}

.remove-btn {
  background-color: #f44336; /* Red color */
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.remove-btn:hover {
  background-color: #d32f2f; /* Darker red color on hover */
}

.search-input {
  margin-bottom: 20px;
}
</style>
