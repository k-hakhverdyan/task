<template>
  <div class="allContent">
    <h1>Customers</h1>
    <input type="text" v-model="search" @keyup="searchData()" class="inputField" placeholder="Search">
    <div class="tableContent">

      <table>
        <thead>
          <tr>
            <th>First Name <i class="fa" :class="{'fa-arrow-down': arrowStatus[0] , 'fa-arrow-up': !(arrowStatus[0])}" @click="sortData(0)" aria-hidden="true"></i></th>
            <th>Last Name <i class="fa" :class="{'fa-arrow-down': arrowStatus[1], 'fa-arrow-up': !arrowStatus[1]}" @click="sortData(1)" aria-hidden="true"></i></th>
            <th>Phone <i class="fa" :class="{'fa-arrow-down': arrowStatus[2], 'fa-arrow-up': !arrowStatus[2]}" @click="sortData(2)" aria-hidden="true"></i></th>
            <th>Email <i class="fa" :class="{'fa-arrow-down': arrowStatus[3], 'fa-arrow-up': !arrowStatus[3]}" @click="sortData(3)" aria-hidden="true"></i></th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item of customers">
            <td>{{item.firstName}}</td>
            <td>{{item.lastName}}</td>
            <td>{{item.phone}}</td>
            <td>{{item.email}}</td>
            <td><button @click="deleteItem(item)" >Delete</button></td>
          </tr>
        </tbody>
      </table>
    </div>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data () {
    return {
      search: '',
      arrowStatus: [false, false, false, false],
      customers: [
        {
          id: 1,
          firstName: 'Balan',
          lastName: 'Groov',
          phone: 145616696,
          email: 'hkexafhhmple@mail.ru',

        },
        {
          id: 2,
          firstName: 'Dan',
          lastName: 'Name',
          phone: 151616151,
          email: 'examphfhfhjle@mail.ru',
        },
        {
          id: 3,
          firstName: 'Eclair',
          lastName: 'Gan',
          phone: 1625450,
          email: 'gexhfhample@mail.ru',
        },
        {
          id: 4,
          firstName: 'Cupcake',
          lastName: 'Kevin',
          phone: 4656947,
          email: 'qexadghmple@mail.ru',
        },
        {
          id: 5,
          firstName: 'Gingerbread',
          lastName: 'Brook',
          phone: 1565966,
          email: 'bexampddle@mail.ru',
        },
        {
          id: 6,
          firstName: 'Jelly',
          lastName: 'Mark',
          phone: 5465452332,
          email: 'exampfle@mail.ru',
        },
        {
          id: 7,
          firstName: 'Lollipop',
          lastName: 'Sem',
          phone: 12332,
          email: 'kexample@mail.ru',
        },
        {
          id: 8,
          firstName: 'Honeycomb',
          lastName: 'Book',
          phone: 12332132,
          email: 'example@mail.ru',
        },
        {
          id: 9,
          firstName: 'Donut',
          lastName: 'Div',
          phone: 12332332,
          email: 'xexxample@mail.ru',
        },
        {
          id: 10,
          firstName: 'KitKat',
          lastName: 'Sati',
          phone: 1233212332,
          email: 'pexample@mail.ru',
        },
      ]
    }
  },
  methods : {
    deleteItem(item) {
      this.customers = this.customers.filter(function (value){return value != item})
    },
    searchData () {
      let tr = this.$el.childNodes[2].childNodes[0].childNodes[1].childNodes;
      let filter = this.search.toLowerCase();
      let cell;
      for(let i = 0; i < tr.length; i++)
      {
        tr[i].style.display = "none";
        let td = tr[i].childNodes
        for(let j = 0; j < td.length - 1; j++)
        {
          cell = td[j]
          if (cell)
          {
              if(cell.innerHTML.toLowerCase().indexOf(filter) > -1)
              {
                tr[i].style.display = "";
              }
          }
        }
      }
    },
    sortData (id) {
      this.arrowStatus = this.arrowStatus.slice(0,id).concat([!this.arrowStatus[id]].concat(this.arrowStatus.slice(id + 1,4)));
      let table,rows,x,y,shoudSwitch,switching,i
      table = this.$el.childNodes[2].childNodes[0]
      switching = true
      while (switching)
      {
        switching = false
        rows = table.rows;
        for(i = 1; i < rows.length - 1; i++)
        {
          shoudSwitch = false
          x = rows[i].childNodes[id]
          y = rows[i + 1].childNodes[id]
          if(this.arrowStatus[id]) {
            if (x.innerHTML.toLowerCase() < y.innerHTML.toLowerCase())
            {
              shoudSwitch = true
              break
            }
          }
          else{
            if (x.innerHTML.toLowerCase() > y.innerHTML.toLowerCase())
            {
              shoudSwitch = true
              break
            }
          }
        }
        if (shoudSwitch)
        {
          console.log(1111)
          rows[i].parentNode.insertBefore(rows[i + 1],rows[i])
          switching = true
        }
      }


    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
  .tableContent {
    display: flex;
    justify-content: center;
  }
  th, td{
    border: 1px solid;
    padding: 5px 10px;
  }
  table {
    border-spacing:  0.8px;
  }
  th {
    font-size: 20px;
    color: #2c3e50;
    background-color: aquamarine;
  }
  tbody tr{
    background-color: cornsilk;
  }
  tbody tr:hover{
    background-color: #aa9a75;
    color: white;
  }

  tbody tr td:last-child {
    padding: 0;
  }
  button {
    width: 100%;
    height: 100%;
    border: none;
    background-color: #DF6378;
    cursor: pointer;

  }
  button:hover {
    background-color: brown;
    color: aliceblue;

  }
  .inputField {
    margin-bottom: 20px;
    width: 200px;
    padding: 5px;
    border: 2px solid #277b7f;
    border-radius: 5px;
  }
  th i {
    width: 30px;
    height: 30px;
    margin: 5px;
    color: #2c3e50;
  }
  .fa {
    width: 30px;
    height: 30px;
    cursor: pointer;
  }
</style>
