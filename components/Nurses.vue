<!-- Please remove this file from your project -->
<template>
  <section class="text-gray-600 body-font">
    <div class="container px-5 pt-12 mx-auto">
      <div class="flex flex-wrap w-full flex-row justify-between">
        <span>
          <NuxtLink to="/home">
            <div
              class="w-10 h-10 inline-flex items-center justify-center rounded-full bg-indigo-100 text-indigo-500 mb-4"
            >
              <svg
                fill="none"
                stroke="currentColor"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                class="w-6 h-6"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M10 19l-7-7m0 0l7-7m-7 7h18"
                />
              </svg>
            </div>
          </NuxtLink>
        </span>
      </div>
    </div>
    <div class="container px-5 pt-12 pb-24 mx-auto">
      <div
        class="flex flex-wrap w-full mb-20 flex-col items-center text-center"
      >
        <h1
          class="sm:text-3xl text-2xl font-medium title-font mb-2 text-gray-900 tracking"
        >
          Nurses
        </h1>
      </div>
      <div class="flex flex-wrap justify-center">
        <div class="container px-5 py-24 mx-auto">
          <div class="lg:w-4/5 mx-auto flex flex-wrap">
            <div class="lg:w-full w-full lg:pr-10 lg:py-6 mb-6 lg:mb-0">
              <div class="flex mb-4">
                <a
                  class="flex-grow text-indigo-500 border-b-2 border-indigo-500 py-2 text-lg px-1"
                  >Nurses List</a
                >
              </div>

              <span v-if="nurses.length">
                <div
                  class="flex border-t border-gray-200 py-2"
                  v-for="item in nurses"
                  :key="item.id"
                >
                  <span class="text-gray-500"
                    >{{ item.narrative }}
                  </span>
                  <span class="ml-auto text-gray-900">{{ item.date }}</span>
                </div>
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Patients',
  data() {
    return {
      username: '',
      email: '',
      first_name: '',
      last_name: '',
      default_currency: '',
      editable: false,
      selected_currency: '',
      profile: {},
      transactions: {},
    }
  },
  methods: {
    updateInfo() {
      axios
        .get('/api/user')
        .then((response) => {
          this.user = response.data
        })
        .catch((error) => {
          console.log(error)
        })
    },
    save() {

      if (this.default_currency == '') {
        this.$toast.show("Please select a currency")
        return
      }

      const params = {
        headers: {
          Accept: 'application/json',
          'Content-Type': 'application/json',
          'Access-Control-Allow-Origin': '*',
          'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE, OPTIONS',
          'Access-Control-Allow-Headers': '*'
        },
      }

      const payload = {
        default_currency: this.selected_currency,
      }

      const BASE_URL = 'http://localhost:8000'
      const userId = localStorage.getItem('userId')

      axios
        .create(params)
        .put(`${BASE_URL}/api/v1/profile/${userId}`, payload)
        .then((response) => {
          console.log(response)
          this.default_currency = this.selected_currency
          this.editable = false
        })
        .catch((error) => {
          console.log(error)
          this.editable = false
        })


      const [transactions] = Promise.all([
        axios.create(params).get(`${BASE_URL}/history`),
      ])
      this.transactions = transactions?.data;
      console.log(this.transactions)

    },
    selected(e) {
      console.log(e.target.value)
      this.selected_currency = e.target.value
    },
  },

  async mounted() {
    try {
      const params = {
        headers: {
          Accept: 'application/json',
          'Content-Type': 'application/json',
          'Access-Control-Allow-Origin': '*',
          'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE, OPTIONS',
          'Access-Control-Allow-Headers': '*'
        },
      }

      const BASE_URL = 'http://localhost:8000'

      const [nurses] = await Promise.all([
        axios.create(params).get(`${BASE_URL}/nurses`),
      ]);
      
      this.nurses = nurses?.data;
      
    } catch (error) {
      console.log(error)
      this.$toast.show('Error fetching data')
    }
  },

}
</script>
