<template>
    <div>
    <div class="tables-container">
      <div class="table-container">
        <table class="custom-table table">
          <!-- Table headers -->
          <thead>
            <tr class="text-black">
              <th>Name</th>
              <th>Type</th>
              <th>Color</th>
              <th>Size</th>
              <th>Price Per Unit</th>
              <th>Quantity</th>
              <th>Design</th>
            </tr>
          </thead>
          <!-- Table body -->
          <tbody>
            <tr v-for="product in orderedProducts.products" :key="product.OrderProductsID">
              <td>{{ product.ProductName }}</td>
              <td>{{ product.ProductType }}</td>
              <td>{{ product.ProductColor }}</td>
              <td>{{ product.ProductSize }}</td>
              <td>${{ product.ProductPrice.toFixed(2) }}</td>
              <td>{{ product.Quantity }}</td>
              <td><v-img :src="product.ProductImage" cover /></td>
            </tr>
          </tbody>
        </table>
        </div>
      </div>
    </div>
  </template>
  
  
  

  <script>
  import axios from "axios";
  
  export default {
    props: {
    OrderID: {
      type: String, 
      required: true
    }
  },
    data() {
      return {
        orderedProducts: [],
      };
    },
    mounted() {
      axios.get(`https://coogtech-backend.vercel.app/customerData/Orders/${this.OrderID}/products`)
        .then(response => {
            console.log(response.data)
          this.orderedProducts = response.data;
        })
        .catch(error => {
          console.error("Error fetching ordered products:", error);
        });
    }
  };
  </script>

<style>
.table-container table tbody tr:hover {
  background-color: #ddd;
}

.table-container {
  background-color: #ffffff; /* White background color */
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.1); /* Subtle box shadow for embossed effect */
}

.table-header {
  text-align: center;
  font-size: 24px;
  color: #333; /* Dark color for the headers */
  margin-bottom: 10px; /* Add space between header and table */
}

.table-container table tbody tr:hover {
  background-color: #ddd;
}

.table-container {
  background-color: #ffffff; /* White background color */
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.1); /* Subtle box shadow for embossed effect */
}


</style>