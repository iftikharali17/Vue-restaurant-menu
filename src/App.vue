<template>
  <div id="app">
   
    <div class="flex justify-between flex-wrap">
      <div class="card">
        <div
          class="max-w-sm rounded overflow-hidden shadow-lg m-10"
          v-for="dish in dishes"
          :key="dish._id"
        >
          <div class="px-6 py-4">
            <div
              class="font-bold text-xl mb-2 flex justify-between item-center"
            >
              <div>{{ dish.data.name }}</div>
              <div class="flex">
                <img
                  class="w-5 m-2"
                  src="../pen-to-square-solid.svg"
                  alt=""
                  @click="() => updateDish(dish)"
                />
                <img
                  class="w-5 m-2"
                  src="../delete-left-solid.svg"
                  alt=""
                  @click="() => deleteDish(dish)"
                />
              </div>
            </div>
            <p class="text-gray-700 text-base">
              {{ dish.data.desc }}
            </p>
          </div>
          <div class="px-6 pt-4 pb-2">
            <span
              class="
                inline-block
                bg-gray-200
                rounded-full
                px-3
                py-1
                text-sm
                font-semibold
                text-gray-700
                mr-2
                mb-2
              "
            >
              <span v-if="dish.data.dishStatus">
                 {{ dish.data.availability }} : Available</span
              >
              <span v-else> {{ dish.data.availability }} : Not available </span>
            </span>
            <span
              class="
                inline-block
                bg-gray-200
                rounded-full
                px-3
                py-1
                text-sm
                font-semibold
                text-gray-700
                mr-2
                mb-2
              "
              > Category: {{ dish.data.category }}</span
            >
            <span
              class="
                inline-block
                bg-gray-200
                rounded-full
                px-3
                py-1
                text-sm
                font-semibold
                text-gray-700
                mr-2
                mb-2
              "
            >
              Waiting time: {{ dish.data.timeToCook }} 
            </span>
            <span
              class="
                inline-block
                bg-gray-200
                rounded-full
                px-3
                py-1
                text-sm
                font-semibold
                text-gray-700
                mr-2
                mb-2
              "
            >
             Price: €{{ dish.data.price }} 
            </span>
          </div>
        </div>
      </div>
      <div class="form p-5 w-96">
        <button
          type="submit"
          class="
            px-6
            py-2.5
            bg-blue-600
            text-white
            font-medium
            text-xs
            leading-tight
            uppercase
            rounded
            shadow-md
            hover:bg-blue-700 hover:shadow-lg
            focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0
            active:bg-blue-800 active:shadow-lg
            transition
            duration-150
            ease-in-out
          "
          @click="toggle = !toggle"
        >
          ADD RECIPE
        </button>
        <div
          class="block p-6 rounded-lg shadow-lg bg-white max-w-sm"
          v-show="toggle"
        >
          <form @submit.prevent="createDish">
            <div class="form-group mb-6">
              <input
                type="text"
                v-model="name"
                class="
                  form-control
                  block
                  w-full
                  px-3
                  py-1.5
                  text-base
                  font-normal
                  text-gray-700
                  bg-white bg-clip-padding
                  border border-solid border-gray-300
                  rounded
                  transition
                  ease-in-out
                  m-0
                  focus:text-gray-700
                  focus:bg-white
                  focus:border-blue-600
                  focus:outline-none
                "
                id="exampleInputEmail1"
                aria-describedby="emailHelp"
                placeholder="Name"
              />
            </div>
            <div class="form-group mb-6">
              <input
                v-model="desc"
                type="text"
                class="
                  form-control
                  block
                  w-full
                  px-3
                  py-1.5
                  text-base
                  font-normal
                  text-gray-700
                  bg-white bg-clip-padding
                  border border-solid border-gray-300
                  rounded
                  transition
                  ease-in-out
                  m-0
                  focus:text-gray-700
                  focus:bg-white
                  focus:border-blue-600
                  focus:outline-none
                "
                id="exampleInputPassword1"
                placeholder="Short description"
              />
            </div>
            <div class="form-group mb-6">
              <label
                for="countries"
                class="
                  block
                  mb-2
                  text-sm
                  font-medium
                  text-gray-900
                  dark:text-gray-400
                "
                >Menu Time
              </label>
              <select
                v-model="availability"
                id="countries"
                class="
                  bg-gray-50
                  border border-gray-300
                  text-gray-900 text-sm
                  rounded-lg
                  focus:ring-blue-500 focus:border-blue-500
                  block
                  w-full
                  p-2.5
                  dark:bg-gray-700
                  dark:border-gray-600
                  dark:placeholder-gray-400
                  dark:text-white
                  dark:focus:ring-blue-500
                  dark:focus:border-blue-500
                "
              >
                <option selected>Choose</option>
                <option value="Breakfast">Breakfast</option>
                <option value="Dinner">Dinner</option>
                <option value="Lunch">Lunch</option>
                <option value="Weekdays/-ends">Weekdays/-ends</option>
              </select>
            </div>
            <div class="form-group mb-6">
              <label
                for="countries"
                class="
                  block
                  mb-2
                  text-sm
                  font-medium
                  text-gray-900
                  dark:text-gray-400
                "
                >Category
              </label>
              <select
                v-model="category"
                id="countries"
                class="
                  bg-gray-50
                  border border-gray-300
                  text-gray-900 text-sm
                  rounded-lg
                  focus:ring-blue-500 focus:border-blue-500
                  block
                  w-full
                  p-2.5
                  dark:bg-gray-700
                  dark:border-gray-600
                  dark:placeholder-gray-400
                  dark:text-white
                  dark:focus:ring-blue-500
                  dark:focus:border-blue-500
                "
              >
                <option selected>Choose</option>
                <option value="Starter">Starter</option>
                <option value="Main course">Main course</option>
                <option value="Dessert">Dessert</option>
                <option value="Beverage">Beverage</option>
              </select>
            </div>
            <div class="form-group mb-6">
              <div class="mt-5">Available</div>
              <div class="flex justify-center">
                <label class="switch">
                  <input type="checkbox" checked v-model="dishStatus" />
                  <span class="slider round"></span>
                </label>
              </div>
            </div>
            <div class="form-group mb-6">
              <input
                v-model="timeToCook"
                type="text"
                class="
                  form-control
                  block
                  w-full
                  px-3
                  py-1.5
                  text-base
                  font-normal
                  text-gray-700
                  bg-white bg-clip-padding
                  border border-solid border-gray-300
                  rounded
                  transition
                  ease-in-out
                  m-0
                  focus:text-gray-700
                  focus:bg-white
                  focus:border-blue-600
                  focus:outline-none
                "
                id="exampleInputPassword1"
                placeholder="Time to cook  "
              />
              <input
                v-model="price"
                type="number"
                class="
                  mt-5
                  form-control
                  block
                  w-full
                  px-3
                  py-1.5
                  text-base
                  font-normal
                  text-gray-700
                  bg-white bg-clip-padding
                  border border-solid border-gray-300
                  rounded
                  transition
                  ease-in-out
                  m-0
                  focus:text-gray-700
                  focus:bg-white
                  focus:border-blue-600
                  focus:outline-none
                "
                id="exampleInputPassword1"
                placeholder="Price"
              />
            </div>
            <button
              type="submit"
              class="
                px-6
                py-2.5
                bg-blue-600
                text-white
                font-medium
                text-xs
                leading-tight
                uppercase
                rounded
                shadow-md
                hover:bg-blue-700 hover:shadow-lg
                focus:bg-blue-700
                focus:shadow-lg
                focus:outline-none
                focus:ring-0
                active:bg-blue-800 active:shadow-lg
                transition
                duration-150
                ease-in-out
              "
              :class="{ 'opacity-50 cursor-not-allowed': !validateFields() }"
              :disabled="!validateFields()"
            >
              Submit
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      toggle: false,
      dishes: [],
      name: "",
      price: "",
      desc: "",
      availability: "",
      category: "",
      dishStatus: false,
      timeToCook: "",
      selectedDish: null,
    };
  },
  mounted() {
    this.getDishes();
  },
  methods: {
    validateFields() {
      return (
        this.name &&
        this.desc &&
        this.availability &&
        this.category &&
        this.timeToCook &&
        this.price
      );
    },
    formFields() {
      this.name = "";
      this.desc = "";
      this.availability = "";
      this.category = "";
      this.dishStatus = false;
      this.timeToCook = "";
      this.price = "";
    },
    async getDishes() {
      const {
        data: { data },
      } = await axios.get("http://localhost:9000/dishes");
      this.dishes = data;
    },
    async deleteDish({ _id }) {
      const deleted = await axios.delete(`http://localhost:9000/dishes/${_id}`);
      this.dishes = this.dishes.filter((dish) => dish._id !== _id);
      console.log({ deleted });
    },
    async createDish() {
      if (!this.validateFields()) return;
      const {
        data: { data: newDish },
      } = await axios.put("http://localhost:9000/dishes", {
        data: {
          name: this.name,
          desc: this.desc,
          availability: this.availability,
          category: this.category,
          dishStatus: this.dishStatus,
          timeToCook: this.timeToCook,
          price: this.price,

          _id: this.selectedDish,
        },
      });

      if (this.selectedDish) {
        this.dishes = this.dishes.map((dish) =>
          dish._id !== this.selectedDish ? dish : newDish
        );
      }
      console.log(newDish);
      if (!this.selectedDish) this.dishes.unshift(newDish);
      this.selectedDish = null;
      this.formFields();
    },

    updateDish({
      _id,
      data: {
        name,
        desc,
        availability,
        category,
        dishStatus,
        timeToCook,
        price,
      },
    } = {}) {
      console.log("update", name, _id);
      this.name = name;
      this.desc = desc;
      this.availability = availability;
      this.category = category;
      this.dishStatus = dishStatus;
      this.timeToCook = timeToCook;
      this.price = price;
      this.selectedDish = _id;
    },
  },
};
</script>
<style>
  #app {
    background-image: url('./assets/background-med.jpg');
    background-size: cover;
  }
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

input:checked + .slider {
  background-color: #2196f3;
}

input:focus + .slider {
  box-shadow: 0 0 1px #2196f3;
}

input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

/* Rounded sliders */
.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
</style>