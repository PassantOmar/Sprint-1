<template>
    <div class="row">
      <div class="col-md-12">
        <div class="card">


          <h2>Products</h2>
          <table style="width:100%">
            <thead>
              <tr>
                <th>ID</th>
                <th>Name</th>
                <th>Price</th>
                <th>CreatedAt</th>
                <th>UpdatedAt</th>
                <th>SellerName</th>
                <th>Actions</th>

              </tr>
            </thead>
            <tbody>
              <tr v-for="row in item.data">
                <td>{{row._id}}</td>
                <td>{{row.name}}</td>
                <td>{{row.price}}</td>
                <td>{{row.createdAt}}</td>
                <td>{{row.updatedAt}}</td>
                <td>{{row.SellerName}}</td>
                <td>{{row.Actions}}</td>
              </tr>


            </tbody>

          </table>
          <form>
            name:<br>
            <input type="text" name="firstname"><br>
            price:<br>
            <input type="text" name="lastname">
          </form>

            <button v-on: click = "post"> add product</button>
          </div>
        </div>

      </div>

</template>
<script>

import axios from 'axios'
const tableColumns = ['Id', 'Name', 'Price', 'CreatedAt', 'UpdatedAt', 'SellerName', 'Action', '']
const tableData = [{
}]

export default {
  data () {
    return {
      table: {
        columns: [...tableColumns],
        data: [...tableData]
      },
      item: [],
      name: '',
      price: ''
    }
  },
  Created () {
    this.getProducts()
  },

  methods: {
    post () {
      axios.post('http://localhost:3000/product/createProduct', {
        name: this.name,
        price: this.price
      }).then((response) => {
        console.log(response)
      })
    .catch((error) => {
      console.log(error)
    })
    },
    getProducts () {
      axios.get('http://localhost:3000/product/getProducts')
      .then((response) => {
        this.item = response.data
        console.log(response)
      })
    .catch((error) => {
      console.log(error)
    })
    }
  }
}

</script>
<style>

</style>
