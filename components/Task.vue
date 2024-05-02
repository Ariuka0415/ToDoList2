<template>
  <!-- Remove inline css -->
  <div class="main">
    <form id="form" @submit.prevent="onSubmit(text)">
      <!-- input width deer anhaarnaa -->
      <~
        v-model="text"
        type="text"
        id="text"
        placeholder="Enter your task...."
      />
    </form>
    <section>
      <ul class="lists">
        <li v-for="(item, index) in list" :key="item.text" class="ul-list">
          <div>
            <input type="checkbox" class="custom-checkbox" />
            {{ item.text }}
          </div>

          <!-- button ii css anhaarnaa -->
          <button @click="deleteItem(index)" class="remove">
            <!-- SVG icon oruulj iree -->
            <img
              src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSUHE5orhlcix_eBdGWPC993wtY_IONYHhb4WAOJUbFfg&s"
              alt=""
            />
          </button>
        </li>
      </ul>
    </section>
  </div>
  <button @click="onSubmit(text)" class="button">Add</button>
</template>

<script setup>
const text = ref("");

const list = ref([]);

const onSubmit = (value = "aav") => {
  // value hooson bvl list ruu push hiihgue
  // value bvl list dotor adilhan utga shalganaa
  if (!value) {
    alert("ajilgui novsh!");
  } else {
    const existingvalue = list.value.find((val) => val.text === value);
    if (existingvalue) {
      alert("This value already exists!");
    } else {
      list.value.push({
        text: value,
      });
    }
  }
  text.value = "";

  //   list ruu add hiisnii daraa text valueg reset
};
// deleteItem: check param
const deleteItem = (index) => {
  list.value.splice(index, 1);
  console.log(index);
};
</script>

<style scoped>
.button {
  background: #ab7ae6;
  border-color: #ab7ae6;
  border-radius: 20px;
  width: 12%;
  height: 40px;
  cursor: pointer;
  transition: 0.3s;
  color: #fff;
  font-size: 19px;
}

ul li {
  padding-bottom: 20px;
  font-size: 30px;
  color: #5e388d;
}
.button :hover {
  background: #5e388d;
}
input {
  margin: 15px;
  width: 48%;
  padding: 10px;
  border: none;
  font-size: 20px;
  color: #5e388d;
  text-decoration: none;
  width: 80%;
  border: none;
  outline: none;
  margin: auto;
}
.listButton {
  border: none;
}
.ul-list {
  display: flex;
  justify-content: space-between;
}
.remove {
  background: none;
  border: none;
  font-size: 30px;
  color: #5e388d;
  cursor: pointer;
  padding-right: 20px !important;
}
.remove:hover {
  color: #cebae7;
}
.main {
  background: #fff;
  width: 50%;
  margin: auto;
}
img {
  width: 20px;
  height: 20px;
}
.custom-checkbox {
  margin-right: 10px;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  width: 15px;
  height: 15px;
  border-radius: 50%;
  border: 1px solid #5e388d;
  background-color: transparent;
  cursor: pointer;
}

.custom-checkbox:checked {
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  background-color: #5e388d;
}
</style>
