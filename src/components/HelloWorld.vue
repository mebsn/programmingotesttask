<template>
  <div id="container">
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
      spiralArray: [],
    };
  },
  methods: {
    createArray(n, m) {
      let array = [];
      for (let i = 1; i < n * m + 1; i++) {
        array.push(i);
      }
      this.mainArray = array;
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
    spiralOrder(m,n,a) {
      let val = 1;
    let k = 0, l = 0;
    while (k < m && l < n)
    {
        for (let i = l; i < n; ++i)
            a[k][i] = val++;
 
        k++;
        for (let i = k; i < m; ++i)
            a[i][n-1] = val++;
        n--;
 
        if (k < m)
        {
            for (let i = n - 1; i >= l; --i)
                a[m-1][i] = val++;
            m--;
        }
        if (l < n)
        {
            for (let i = m - 1; i >= k; --i)
                 a[i][l] = val++;
            l++;
        }
    }
    this.spiralArray = a;
    },
    async createTable() {
      document.getElementById("myTable").innerHTML= "";
      this.createArray(this.row, this.column);
      this.chunk(this.mainArray, this.column);

      let rn = this.row;
      let cn = this.column;
      console.log(rn);
      console.log(cn);
      let a = Array.from(Array(parseInt(rn, 10)), () => new Array(parseInt(cn, 10)));

      this.spiralOrder(this.row,this.column,a);

      for (var r = 0; r < parseInt(rn, 10); r++) {
        var x = document.getElementById("myTable").insertRow(r);
        for (var c = 0; c < parseInt(cn, 10); c++) {
          var y = x.insertCell(c);
          y.innerHTML = this.spiralArray[r][c];
          y.style.width = "50px";
          y.style.height = "50px";
          y.style.color = "white"
          if ( 40*this.spiralArray[r][c] < 256){
            y.style.backgroundColor = `rgba(${40*this.spiralArray[r][c]},0,0 )`;

          }
          else if ( 40*this.spiralArray[r][c] > 255 && 40*this.spiralArray[r][c] < 511) {
            y.style.backgroundColor = `rgba(0,${(40*this.spiralArray[r][c])-255},0 )`;
          }
          else if ( 40*this.spiralArray[r][c] > 510) {
            y.style.backgroundColor = `rgba(0,0,${40*this.spiralArray[r][c]-510} )`;
          }
        }
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#container {
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
