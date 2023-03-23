<template>
  <div class="content">
    <router-link to="add"><button>Add new order</button></router-link>
    <div class="filters">
      <input type="text" v-model="search" placeholder="Search">
      <select v-model="selectedStatus">
        <option>All Status</option>
        <option>Confirmed</option>
        <option>In delivering</option>
        <option>Delivered</option>
      </select>
    </div>
    <table>
      <thead>
        <tr>
          <th @click="sort('date')">Date</th>
          <th @click="sort('sender')">Sender</th>
          <th @click="sort('destination')">Destination</th>
          <th>Status</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="order in filteredOrders" :key="order.id">
          <td>{{ order.date }}</td>
          <td>{{ order.sender }}</td>
          <td>{{ order.destination }}</td>
          <td>{{ order.status }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      search: '',
      selectedStatus: 'All Status',
      sortOrder: 'asc',
      sortBy: '',
      orders: [
        {
          id: 1,
          date: "2023/03/12",
          sender: "Gerlach-Sanford",
          destination: "Cole-Armstrong",
          status: "Delivered",
          weight: 8
        },
        {
          id: 2,
          date: "2023/03/11",
          sender: "Von-Satterfield",
          destination: "Purdy, Reichert and Ritchie",
          status: "Delivered",
          weight: 1
        },
        {
          id: 3,
          date: "2023/03/11",
          sender: "Lowe and Sons",
          destination: "Goodwin and Sons",
          status: "Confirmed",
          weight: 2
        },
        {
          id: 4,
          date: "2023/03/05",
          sender: "Sawayn-Streich",
          destination: "Rohan Group",
          status: "Delivered",
          weight: 1
        },
        {
          id: 5,
          date: "2023/03/05",
          sender: "Durgan-Koch",
          destination: "Rosenbaum, Parker and Willms",
          status: "Delivered",
          weight: 4
        },
        {
          id: 6,
          date: "2023/03/11",
          sender: "Christiansen, Treutel and Kirlin",
          destination: "Barrows, Glover and Dibbert",
          status: "Confirmed",
          weight: 1
        },
        {
          id: 7,
          date: "2023/03/06",
          sender: "Corwin-Kovacek",
          destination: "Johnston Group",
          status: "Delivered",
          weight: 10
        },
        {
          id: 8,
          date: "2023/03/22",
          sender: "Ullrich-Bashirian",
          destination: "Okuneva and Sons",
          status: "Confirmed",
          weight: 1
        },
        {
          id: 9,
          date: "2023/03/09",
          sender: "Hermiston Inc",
          destination: "Ruecker LLC",
          status: "Delivered",
          weight: 1
        },
        {
          id: 10,
          date: "2023/03/30",
          sender: "Mills, Sporer and Kohler",
          destination: "Connelly-Steuber",
          status: "Delivered",
          weight: 4
        }
      ]
    }
  },
  computed: {
    filteredOrders() {
      let filtered = this.orders.filter(order => {
        return (
          (order.sender.toLowerCase().includes(this.search.toLowerCase()) ||
            order.destination.toLowerCase().includes(this.search.toLowerCase())) &&
          (this.selectedStatus === 'All Status' || order.status === this.selectedStatus)
        )
      })

      if (this.sortBy) {
        filtered.sort((a, b) => {
          if (this.sortOrder === 'asc') {
            return a[this.sortBy] > b[this.sortBy] ? 1 : -1
          } else {
            return a[this.sortBy] < b[this.sortBy] ? 1 : -1
          }
        })
      }

      return filtered
    }
  },
  methods: {
    sort(field) {
      if (this.sortBy === field) {
        this.sortOrder = this.sortOrder === 'asc' ? 'desc' : 'asc'
      } else {
        this.sortBy = field
        this.sortOrder = 'asc'
      }
    }
  }
}
</script>
