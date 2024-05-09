<template>
  <div class="main1">
    <form class="element" @submit.prevent="onSubmit(text)">
      <input
        v-model="text"
        type="text"
        id="text"
        placeholder="Enter your task...."
      />
    </form>
    <section class="element">
      <ul class="lists">
        <li v-for="(item, index) in list" :key="item.text" class="ul-list">
          <div>
            <input type="checkbox" class="custom-checkbox" />
            <input
              v-if="item.editing"
              v-model="item.updatedText"
              @blur="updateItem(index)"
            />
            <span v-else>{{ item.text }}</span>
          </div>
          <div>
            <button @click="deleteItem(index)" class="remove">
              <img
                src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSUHE5orhlcix_eBdGWPC993wtY_IONYHhb4WAOJUbFfg&s"
                alt=""
              />
            </button>
            <button @click="editItem(index)" class="remove">
              <img
                src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTvr2HodSelXZZK8FAB9hhO0ShvUazNWWXERbL407ccFA&s"
                alt=""
              />
            </button>
          </div>
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
  if (!value) {
    alert("Хоосон байна! ");
  } else {
    const existingvalue = list.value.find((val) => val.text === value);
    if (existingvalue) {
      alert("This value already exists!");
    } else {
      list.value.push({
        text: value,
      });
      localStorage.setItem("tasks", JSON.stringify(list.value));
    }
  }
  text.value = "";
};

onMounted(() => {
  list.value = JSON.parse(localStorage.getItem("tasks"));
});
// deleteItem: check param
const deleteItem = (index) => {
  list.value.splice(index, 1);
  localStorage.setItem("tasks", JSON.stringify(list.value));
};

// UpdateItem
const updateItem = (index) => {
  const newText = list.value[index].updatedText.trim();
  if (!newText) {
    alert("Task cannot be empty");
  } else {
    list.value[index].text = newText;
    list.value[index].editing = false;
    localStorage.setItem("tasks", JSON.stringify(list.value));
    alert("Updated!");
  }
};

const editItem = (index) => {
  list.value[index].editing = true;
  list.value[index].updatedText = list.value[index].text;
};
</script>

<style scoped>
.main1 {
  background: #fff;
  width: 70%;
  margin: auto;
  margin-top: 80px;
}
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
  margin-bottom: 30px !important;
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

#button {
  float: right !important;
}

@media (max-width: 600px) {
  .main1 {
    font-size: 20px;
  }
}
</style>
