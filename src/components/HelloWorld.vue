<template>
  <div class="container">
    <input type="number" placeholder="enter rows" v-model="row" />
    <input type="number" placeholder="enter columns" v-model="column" />
    <div class="create_table" @click="createTable()">Create Table</div>
    <table id="myTable"></table>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      row: null,
      column: null,
      mainArray:[],
    };
  },
  methods: {
    createArray(n,m) {
      let array = [];
      for (let i = 1; i < n * m + 1; i++) {
        array.push(i);
      }
      this.mainArray = array;
      // console.log(this.mainArray);
    },
    formSpiralMatrix() {
    const arr = this.mainArray;
    // console.log("bla", arr);
    let row = 0;
    let col = 0;
    let rowEnd = this.row - 1;
    let colEnd = this.column - 1;
    let counter = 1;
    while (col <= colEnd && row <= rowEnd) {
        for (let i = col; i <= colEnd; i++) {
            arr[row][i] = counter;
            counter++;
        }
        row++;

        for (let i = row; i <= rowEnd; i++) {
            arr[i][colEnd] = counter;
            counter++;
        }
        colEnd--;

        for (let i = colEnd; i >= col; i--) {
            arr[rowEnd][i] = counter;
            counter++;
        }
        rowEnd--;

        for (let i = rowEnd; i >= row; i--) {
            arr[i][col] = counter;
            counter++;
        }
        col++;
    }
    return arr;
    },
    async createTable(){
      await this.createArray(this.row, this.column);
      this.formSpiralMatrix(this.mainArray);
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}
input {
  margin-top: 20px;
  width: 120px;
  height: 25px;
  border-radius: 4px;
}
.create_table {
  width: 160px;
  height: 30px;
  background-color: aqua;
  border-radius: 4px;
  display: flex;
  justify-content: center;
  color: black;
  align-items: center;
  margin-top: 20px;
  cursor: pointer;
}
#myTable {
  margin-top: 70px;
}
</style>
