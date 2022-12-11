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
            <div class="flex justify-end mb-4">
                <button @click="showModal = true" class="relative inline-flex items-center justify-center p-0.5 mb-2 mr-2 overflow-hidden text-sm font-medium text-gray-900 rounded-lg group bg-gradient-to-br from-purple-500 to-pink-500 group-hover:from-purple-500 group-hover:to-pink-500 hover:text-white dark:text-white focus:ring-4 focus:outline-none focus:ring-purple-200 dark:focus:ring-purple-800">
                  <span class="relative px-5 py-2.5 transition-all ease-in duration-75 bg-white dark:bg-gray-900 rounded-md group-hover:bg-opacity-0">
                      Add +
                  </span>
                </button>
              </div>
              <div class="flex mb-4">
                <a
                  class="flex-grow text-indigo-500 border-b-2 border-indigo-500 py-2 text-lg px-1"
                  >Nurses List</a
                >
              </div>

              <span v-if="nurses.length">
                <div
                  class="flex border-b border-gray-200 py-2"
                  v-for="item in nurses"
                  :key="item.id"
                >
                  <span class="text-gray-500"
                    >{{ item.staffCategory}}
                  </span>
                  <span class="ml-auto text-gray-900">{{ item.employmentStatus }}</span>
                </div>
              </span>
              <span v-else>
                No data at the moment.
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!--Create modal -->
    <div class="modal-mask" v-show="showModal">
      <div class="modal-wrapper">
        <div class="modal-container">

          <div class="modal-header">
            <slot name="header">
              default header
            </slot>
          </div>

          <div class="modal-body">
            <slot name="body">
              default body
            </slot>
          </div>

          <div class="modal-footer">
            <slot name="footer">
              default footer
              <button class="modal-default-button" @click="closeModal()">
                Close
              </button>
            </slot>
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
      nurses: [],
      showModal: false,
    }
  },
  methods: {
    closeModal(){
      this.showModal = false;
    },
    create() {
      const params = {
        headers: {
          Accept: 'application/json',
          'Content-Type': 'application/json',
          'Access-Control-Allow-Origin': '*',
          'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE, OPTIONS',
          'Access-Control-Allow-Headers': '*'
        },
      };

      const payload = {
        user_id: localStorage.getItem('user_id'),
        entry: this.type,
        amount: this.amount,
      }

      const BASE_URL = 'http://localhost:8000';

      axios
        .create(params)
        .post(`${BASE_URL}/nurse`, payload)
        .then((response) => {
          console.log(response)
          if (response.data.success) {
            this.$toast.show('successfully created.');
          }
        })
        .catch((error) => {
          console.log(error)
          this.$toast.show('Something went wrong!')
        });
    },
    delete(id) {
      const params = {
        headers: {
          Accept: 'application/json',
          'Content-Type': 'application/json',
          'Access-Control-Allow-Origin': '*',
          'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE, OPTIONS',
          'Access-Control-Allow-Headers': '*'
        },
      };
      const BASE_URL = 'http://localhost:8000';
      axios
        .create(params)
        .delete(`${BASE_URL}/nurse/${id}`,)
        .then((response) => {
          console.log(response)
          if (response.data.success) {
            this.$toast.show('Successfully deleted.')
          }
        })
        .catch((error) => {
          console.log(error)
          this.$toast.show('Something went wrong!')
        })
    }
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
        axios.create(params).get(`${BASE_URL}/nurse`),
      ]);
      
      this.nurses = nurses?.data;
      
    } catch (error) {
      console.log(error)
      this.$toast.show('Error fetching data')
    }
  },

}
</script>
