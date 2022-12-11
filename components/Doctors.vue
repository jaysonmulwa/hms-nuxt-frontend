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
          Doctors
        </h1>
      </div>
      <!--<div class="flex flex-wrap justify-center -m-4">
        <div class="w-full lg:w-3/5 p-4">
          <div
            class="border border-gray-200 p-6 rounded-lg flex flex-wrap justify-center -m-4"
          >
            <span
              class="w-full xl:w-1/2 lg:w-1/2 md:w-1/2 sm:w-full xs:w-full p-4"
            >
              <div class="flex items-center justify-center h-full">
                <div
                  class="w-48 h-48 rounded-full inline-flex items-center justify-center bg-gray-200 text-gray-400"
                >
                  <svg
                    fill="none"
                    stroke="currentColor"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    class="w-24 h-24"
                    viewBox="0 0 24 24"
                  >
                    <path d="M20 21v-2a4 4 0 00-4-4H8a4 4 0 00-4 4v2"></path>
                    <circle cx="12" cy="7" r="4"></circle>
                  </svg>
                </div>
              </div>
            </span>
            <span
              class="w-full xl:w-1/2 lg:w-1/2 md:w-1/2 sm:w-full xs:w-full p-4"
            >
              <div class="flex border-b border-gray-200 py-2">
                <span class="text-gray-500">Username</span>
                <span class="ml-auto text-gray-900">jj19990001</span>
              </div>

              <div class="flex border-b border-gray-200 py-2">
                <span class="text-gray-500">Default Currency</span>
                <span
                  class="ml-auto text-gray-900 flex flex-row"
                  v-if="!editable"
                >
                  <p class="px-2">USD</p>
                  <small @click="editable = true"
                    ><a><u>Edit</u></a></small
                  >
                </span>
                <span
                  class="ml-auto text-gray-900 flex flex-row"
                  v-else-if="editable"
                >
                  <select
                    @change="selected($event)"
                    v-model="default_currency"
                    id="default_currency"
                    class="block w-full px-4 py-2 bg-white border border-gray-400 rounded-lg shadow-sm focus:outline-none focus:shadow-outline-blue focus:border-blue-300 transition duration-150 ease-in-out sm:text-sm sm:leading-5"
                  >
                    <option value="">-- Select a Currency --</option>
                    <option value="USD">USD</option>
                    <option value="KES">KES</option>
                  </select>
                  <small @click="save" class="pl-2"
                    ><a><u>Save</u></a></small
                  >
                </span>
              </div>

              <div class="flex border-b border-gray-200 py-2">
                <span class="text-gray-500">Email address</span>
                <span class="ml-auto text-gray-900"
                  >jayson.mulwa@gmail.com</span
                >
              </div>

              <div class="flex border-b border-gray-200 py-2">
                <span class="text-gray-500">First name</span>
                <span class="ml-auto text-gray-900">Jayson</span>
              </div>

              <div class="flex border-b border-gray-200 py-2">
                <span class="text-gray-500">Last name</span>
                <span class="ml-auto text-gray-900">Mulwa</span>
              </div>
            </span>
          </div>
        </div>
      </div>-->
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
                  >Doctors</a
                >
              </div>

              <span v-if="doctors.length">
                <div
                  class="flex border-b border-gray-200 py-2"
                  v-for="item in doctors"
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
      <!--Create modal -->
      <div class="modal-mask" v-show="showModal">
        <div class="modal-wrapper">
          <div class="modal-container">

            <div class="modal-header">
              <slot name="header">
                <p class="leading-relaxed mb-5 text-gray-600">
                  Add a payment
                </p>
              </slot>
            </div>

            <div class="modal-body">
              <slot name="body">
                  <div class="container flex justify-center">
                  <div
                    class="bg-gray-100 rounded-lg p-8 flex flex-col w-full mt-10 md:mt-0 relative z-10 shadow-md"
                  >
                    
                      <div class="relative mb-4">
                      <label for="title" class="leading-7 text-sm text-gray-600"
                        >Title</label
                      >
                      <input
                        v-model="title"
                        type="text"
                        id="title"
                        name="title"
                        class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                      />
                    </div>
                    <div class="relative mb-4">
                      <label for="firstName" class="leading-7 text-sm text-gray-600"
                        >First name</label
                      >
                      <input
                        v-model="firstName"
                        type="text"
                        id="firstName"
                        name="firstName"
                        class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                      />
                    </div>

                    <div class="relative mb-4">
                      <label for="middleName" class="leading-7 text-sm text-gray-600"
                        >Middle name</label
                      >
                      <input
                        v-model="middleName"
                        type="text"
                        id="middleName"
                        name="middleName"
                        class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                      />
                    </div>

                    <div class="relative mb-4">
                      <label for="lastName" class="leading-7 text-sm text-gray-600"
                        >Last name</label
                      >
                      <input
                        v-model="lastName"
                        type="text"
                        id="lastName"
                        name="lastName"
                        class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                      />
                    </div>

                    <div class="relative mb-4">
                      <label for="birthDate" class="leading-7 text-sm text-gray-600"
                        >Date of Birth</label
                      >
                      <input
                        v-model="birthDate"
                        type="date"
                        id="birthDate"
                        name="birthDate"
                        class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                      />
                    </div>

                    <div class="relative mb-4">
                      <label for="gender" class="leading-7 text-sm text-gray-600"
                        >Gender</label
                      >
                      <input
                        v-model="gender"
                        type="text"
                        id="gender"
                        name="gender"
                        class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                      />
                    </div>

                    <div class="relative mb-4">
                      <label for="homeAddress" class="leading-7 text-sm text-gray-600"
                        >Home Address</label
                      >
                      <input
                        v-model="homeAddress"
                        type="text"
                        id="homeAddress"
                        name="homeAddress"
                        class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                      />
                    </div>

                    <div class="relative mb-4">
                      <label for="phone" class="leading-7 text-sm text-gray-600"
                        >Phone</label
                      >
                      <input
                        v-model="phone"
                        type="tel"
                        id="phone"
                        name="phone"
                        class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                      />
                    </div>


                    <div class="relative mb-4">
                      <label for="kinContacts" class="leading-7 text-sm text-gray-600"
                        >Kin Contacts</label
                      >
                      <input
                        v-model="kinContacts"
                        type="text"
                        id="kinContacts"
                        name="kinContacts"
                        class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                      />
                    </div>
                    <button
                      class="text-white bg-indigo-500 border-0 py-2 px-6 focus:outline-none hover:bg-indigo-600 rounded text-lg"
                      @click="create"
                    >
                      Save
                    </button>
                  </div>
                </div>
              </slot>
            </div>

            <div class="modal-footer">
              <slot name="footer">
                .
                <button class="modal-default-button" @click="closeModal()">
                  Close
                </button>
              </slot>
            </div>
          </div>
        </div>
      </div>
      <!--End of create modal-->
    </div>
  </section>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Doctors',
  data() {
    return {
      title: "",
      firstName: "",
      middleName: "",
      lastName: "",
      birthDate: "",
      gender: "",
      homeAddress: "",
      phone: "",
      kinContacts: "",

      profile: {},
      doctors: [],
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
        title: this.title,
        firstName: this.firstName,
        middleName: this.middleName,
        lastName: this.lastName,
        birthDate: this.birthDate,
        gender: this.gender,
        homeAddress: this.homeAddress,
        phone: this.phone,
        kinContacts:this.kinContacts,
      }

      const BASE_URL = 'http://localhost:8000';

      axios
        .create(params)
        .post(`${BASE_URL}/doctor`, payload)
        .then((response) => {
          console.log(response)
          if (response.data.success) {
            this.$toast.show('successfully created.');
            this.showModal = false;
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
        .delete(`${BASE_URL}/doctor/${id}`,)
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

      const [doctors] = await Promise.all([
        axios.create(params).get(`${BASE_URL}/doctor`),
      ])
      this.doctors = doctors?.data;
      
    } catch (error) {
      console.log(error)
      this.$toast.show('Error fetching data')
    }
  },

}
</script>
