<template>
  <div class="hello">
    <div id="header">
      <img src="../assets/heart.png" alt="1" />
      <h1>Vue.js Calorie Counter</h1>
    </div>
    <table>
      <tr>
        <th>DESCRIPTION</th>
        <th>CALORIES</th>
        <th>FAT</th>
        <th>CARBS</th>
        <th>PROTEIN</th>
      </tr>
      <tr v-for="(item, index) in foods" v-bind:key="index">
        <td>{{ item.description }}</td>
        <td>{{ item.cal }}</td>
        <td>{{ item.carbs }}</td>
        <td>{{ item.fat }}</td>
        <td>{{ item.protein }}</td>
        <button v-on:click="removeItem(index)">X</button>
      </tr>
    </table>

    <div class="adding_styles">
      <div>
        <span>Totals:</span>
        <span
          ><strong>{{ totalCalories }}</strong></span
        >
        <span
          ><strong>{{ totalCarbs }}</strong></span
        >
        <span
          ><strong>{{ totalFat }}</strong></span
        >
        <span
          ><strong>{{ totalProtein }}</strong></span
        >
      </div>
    </div>
    <div>
      <input placeholder="Description" v-model="newDescription" type="text" />
      <input placeholder="Calories" v-model="newCalories" type="number" />
      <input placeholder="Carbs" v-model="newCarbs" type="number" />
      <input placeholder="Fat" v-model="newFat" type="number" />
      <input placeholder="Protein" v-model="newProtein" type="number" />
      <button v-on:click="addItem">+</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data: function () {
    return {
        newDescription: "",
        newCalories: "",
        newCarbs: "",
        newFat: "",
        newProtein: "",
        totalCalories: 0,
        totalCarbs: 0,
        totalFat: 0,
        totalProtein: 0,
      foods: [
        {
          description: "Sargarepa",
          calories: 1000,
          carbs: 500,
          fat: 10,
          protein: 100,
        },
        {
          description: "krompir",
          calories: 1000,
          carbs: 500,
          fat: 10,
          protein: 100,
        },
        {
          description: "paradajz",
          calories: 1000,
          carbs: 500,
          fat: 10,
          protein: 100,
        },
      ]
    };
  },
  methods: {
    // Dodaje Novu Hranu
    addItem: function () {
      let description = this.newDescription.trim();
      let calories = parseInt(this.newCalories.trim() || 0);

      if(description && calories) {
        this.foods.push({
          description: this.newDescription,
          calories: this.newCalories,
          carbs: this.newCarbs,
          fat: this.newFat,
          protein: this.newProtein,
        });
        this.newDescription = null;
        this.newCalories = null;
        this.newCarbs = null;
        this.newFat = null;
        this.newProtein = null;
        this.calculatingValues();
      }
    },
    removeItem: function (itemIndex) {
      this.foods.splice(itemIndex, 1);
      this.calculatingValues();
    },
    calculatingValues: function () {
      this.totalCalories = 0;
      this.totalCarbs = 0;
      this.totalFat = 0;
      this.totalProt = 0;
      for (let i = 0; i < this.foods.length; i++) {
        this.totalCalories += parseInt(this.foods[i].calories);
        this.totalCarbs += parseInt(this.foods[i].carbs);
        this.totalFat += parseInt(this.foods[i].fat);
        this.totalProt += parseInt(this.foods[i].protein);
      }
    },
  },
  mounted() {
    this.calculatingValues();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h1 {
  color: #fff;
  display: inline-block;
  margin: 30px 0px;
  font-weight: normal;
}
img {
  height: 80px;
  margin: 20px 0px;
  position: absolute;
  left: 30px;
  top: -10px;
}
#header {
  background-color: rgb(70, 161, 131);
  height: 100px;
  position: relative;
}
table {
  width: 100%;
  text-align: left;
  box-sizing: border-box;
  table th {
    margin: 0px 20px;
    padding: 20px 50px;
    width: 120px;
    display: inline-block;
  }
  table td {
    margin: 0px 20px;
    padding: 20px 50px;
    width: 120px;
    display: inline-block;
    border-bottom: 1px solid rgb(91, 95, 99);
  }
}

table th {
  margin: 0px 20px;
  padding: 20px 50px;
  width: 120px;
  display: inline-block;
}
table td {
  margin: 0px 20px;
  padding: 20px 50px;
  width: 120px;
  display: inline-block;
  border-bottom: 1px solid rgb(91, 95, 99);
}

button {
  margin: 10px;
}

table th:first-child {
  padding-left: 30px;
  margin-left: 50px;
}

span {
  margin: 15px 20px;
  display: inline-block;
}
.adding_styles {
  background-color: grey;
  height: 50px;
  margin: 15px;
}
th {
  padding: 30px 0px;
}
input {
  border: none;
  border-bottom: 1px solid grey;
  margin: 2px;
}
</style>
