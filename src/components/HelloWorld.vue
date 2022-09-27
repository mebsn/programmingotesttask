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
      mainArray: [],
      chunkedArray: [],
      spiralArray:[],
    };
  },
  methods: {
    createArray(n, m) {
      let array = [];
      for (let i = 1; i < n * m + 1; i++) {
        array.push(i);
      }
      this.mainArray = array;
      // console.log(this.mainArray);
    },
    chunk(items, size) {
      const chunks = [];
      items = [].concat(...items);

      while (items.length) {
        chunks.push(items.splice(0, size));
      }
      this.chunkedArray = chunks;
      console.log(this.chunkedArray);
    },
    spiralOrder(matrix) {
      let ans = [];

      if (matrix.length == 0) return ans;

      let R = this.row,
        C = this.column;
      let seen = new Array(R);
      for (let i = 0; i < R; i++) {
        seen[i] = new Array(C);
        for (let j = 0; j < C; j++) {
          seen[i][j] = false;
        }
      }

      let dr = [0, 1, 0, -1];
      let dc = [1, 0, -1, 0];
      let r = 0,
        c = 0,
        di = 0;
      for (let i = 0; i < R * C; i++) {
        ans.push(matrix[r]);
        seen[r] = true;
        let cr = r + dr[di];
        let cc = c + dc[di];

        if (0 <= cr && cr < R && 0 <= cc && cc < C && !seen[cr][cc]) {
          r = cr;
          c = cc;
        } else {
          di = (di + 1) % 4;
          r += dr[di];
          c += dc[di];
        }
      }
      this.spiralArray = ans;
      console.log("bla", this.spiralArray);
    },
    async createTable() {
      this.createArray(this.row, this.column);
      this.chunk(this.mainArray, this.column);
      this.spiralOrder(this.chunkedArray);
    },
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
