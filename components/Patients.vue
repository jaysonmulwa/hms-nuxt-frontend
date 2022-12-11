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
          Patients
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
                  >Patients</a
                >
              </div>

              <span v-if="patients.length">
                <div
                  class="flex border-b border-gray-200 py-2"
                  v-for="item in patients"
                  :key="item.id"
                >
                  <span class="text-gray-500"
                    >{{ item.title}} {{ item.firstName }} {{ item.lastName }} {{ item.middleName }}
                  </span>
                  <span class="ml-auto text-gray-900">{{ item.gender }}</span>
                  <span class="ml-auto text-gray-900">{{ item.age }}</span>
                </div>
              </span>
            </div>
          </div>
        </div>
      </div>
      <div class="flex flex-wrap justify-center">
        <div class="container px-5 py-24 mx-auto">
          <div class="lg:w-4/5 mx-auto flex flex-wrap">
            <div class="lg:w-full w-full lg:pr-10 lg:py-6 mb-6 lg:mb-0">
              
              <div class="flex mb-4">
                <a
                  class="flex-grow text-indigo-500 border-b-2 border-indigo-500 py-2 text-lg px-1"
                  >Recent Patient History</a
                >
              </div>
              <p class="leading-relaxed mb-4">
                This is the most recent patient history.
              </p>

              <span v-if="transactions.length">
                <div
                  class="flex border-b border-gray-200 py-2"
                  v-for="item in transactions"
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

                    <div class="relative mb-4">
                      <label for="age" class="leading-7 text-sm text-gray-600"
                        >Age</label
                      >
                      <input
                        v-model="age"
                        type="number"
                        id="age"
                        name="age"
                        class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                      />
                    </div>

                    <div class="relative mb-4">
                      <label for="weight" class="leading-7 text-sm text-gray-600"
                        >Weight</label
                      >
                      <input
                        v-model="weight"
                        type="number"
                        id="weight"
                        name="weight"
                        class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                      />
                    </div>

                    <div class="relative mb-4">
                      <label for="sickness" class="leading-7 text-sm text-gray-600"
                        >Sickness</label
                      >
                      <input
                        v-model="sickness"
                        type="text"
                        id="sickness"
                        name="sickness"
                        class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                      />
                    </div>

                    <div class="relative mb-4">
                      <label for="prescription" class="leading-7 text-sm text-gray-600"
                        >Prescription</label
                      >
                      <input
                        v-model="prescription"
                        type="text"
                        id="prescription"
                        name="prescription"
                        class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                      />
                    </div>

                    <div class="relative mb-4">
                      <label for="allergies" class="leading-7 text-sm text-gray-600"
                        >Allergies</label
                      >
                      <input
                        v-model="allergies"
                        type="text"
                        id="allergies"
                        name="allergies"
                        class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                      />
                    </div>

                    <div class="relative mb-4">
                      <label for="specialRequests" class="leading-7 text-sm text-gray-600"
                        >Special requests</label
                      >
                      <input
                        v-model="specialRequests"
                        type="text"
                        id="specialRequests"
                        name="specialRequests"
                        class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                      />
                    </div>


                    <button
                      class="text-white bg-indigo-500 border-0 py-2 px-6 focus:outline-none hover:bg-indigo-600 rounded text-lg"
                      @click="create"
                    >
                      Save
                    </button>
                    <p class="text-xs text-gray-500 mt-3">
                      Currency conversions will be handles automatically.
                    </p>
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
  </section>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Patients',
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
      age: 0,
      weight: 0,
      sickness: "",
      prescription: "",
      allergies: "",
      specialRequests: "",
      profile: {},
      transactions: {},
      patients: {},
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
        age: this.age,
        weight: this.weight,
        sickness: this.sickness,
        prescription: this.prescription,
        allergies: this.allergies,
        specialRequests: this.specialRequests
      }

      const BASE_URL = 'http://localhost:8000';

      axios
        .create(params)
        .post(`${BASE_URL}/patients`, payload)
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
        .delete(`${BASE_URL}/patients/${id}`,)
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

      const [patients, transactions] = await Promise.all([
        axios.create(params).get(`${BASE_URL}/patients`),
        axios.create(params).get(`${BASE_URL}/history`),
      ])
      this.transactions = transactions?.data;
      this.patients = patients?.data;
      
    } catch (error) {
      console.log(error)
      this.$toast.show('Error fetching data')
    }
  },

}
</script>
