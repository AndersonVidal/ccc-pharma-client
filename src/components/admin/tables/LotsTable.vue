<template>
  <div>
    <div class="tools-bar">
      <button class='btn-cadastrar' @click='lotForm()'><span class='icon'>{{icons.plus}}</span>  Novo</button>
      <lots-form/>
      <ul class="nav-estoque">
        <li @click="tab = 'estoque'" :class="{active: tab === 'estoque'}">Estoque</li>
        <li @click="tab = 'vencidos'; filterVencidos()" :class="{active: tab === 'vencidos'}">Vencidos</li>
        <li @click="tab = 'em_falta'" :class="{active: tab === 'em_falta'}">Em falta</li>
      </ul>
    </div>
    <table class='table'>
      <thead>
        <tr>
          <th v-for="title in dinamicTitles" :key="title.property"
          @click="sortProperty=title.property">
            {{ title.label }}
            <span v-if="sortProperty === title.property">{{ icons.arrowTriD }}</span>
            <span v-else style="color: #ddd">{{ icons.arrowTriU }}</span>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for='(lote, index) in lotes' :key='index'>
          <td>{{ lote.produto }}</td>
          <td>{{ lote.quantidade }}</td>
          <td>{{ lote.validade }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import LotsForm from '@/components/admin/forms/LotsForm'
import icons from 'glyphicons'

export default {
  name: 'LotsTable',
  data () {
    return {
      icons,
      sortProperty: 'produto',
      tab: 'estoque',
      dinamicTitles: [
        { label: 'Produto', property: 'produto' },
        { label: 'Quantidade', property: 'quantidade' },
        { label: `Validade`, property: 'validade' }
      ],
      lotes: [
        {
          produto: 'Paracetamol',
          quantidade: 15,
          validade: '2020/12/09'
        },
        {
          produto: 'Buscopan',
          quantidade: 30,
          validade: '2020/11/04'
        },
        {
          produto: 'Benegrip',
          quantidade: 10,
          validade: '2020/05/10'
        },
        {
          produto: 'Remedio',
          quantidade: 10,
          validade: '2015/05/10'
        }
      ]
    }
  },
  mounted () {
    this.sort()
  },
  watch: {
    sortProperty () {
      this.sort()
    }
  },
  components: {
    LotsForm
  },
  methods: {
    lotForm () {
      var form = document.getElementById('lotForm')
      form.style.display = 'block'
    },
    sort () {
      this.lotes.sort((a, b) => {
        if (a[this.sortProperty] < b[this.sortProperty]) return -1
        else if (a[this.sortProperty] > b[this.sortProperty]) return 1
        else return 0
      })
    },
    filterVencidos () {
      this.lotes.filter((lote) => {
        return (new Date(lote.validade)) < Date.now()
      })
    }
  }
}
</script>

<style lang='scss' scoped>
.tools-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 2rem 0;
}
.nav-estoque {
  margin: auto;
  user-select: none;
  box-shadow: 0 0 3px #ccc;
  padding: 1rem;
  .active {
    font-weight: 600;
    color: #0fb5d6;
  }
  li {
    list-style: none;
    display: inline-block;
    padding: 0 1rem;
    border-right: 1px solid #ddd;
    color: #aaa;
    cursor: pointer;
    &:last-child {
      border-right: none;
    }
  }
}
.btn-cadastrar {
  background-color: #fff;
  border: none;
  box-shadow: 0 1px 7px #aaa;
  border-radius: 24px;
  padding: .8rem 1.2rem;
  color: #888;
  font-size: .9rem;
  font-weight: bold;
  cursor: pointer;
  outline: none;
}
.icon {
  margin-right: .7rem;
  color: #55b42f;
  font-size: 1rem;
}
table {
  border-collapse: collapse;
  width: 100%;
  thead {
    border-bottom: 1px solid #ddd;
  }
  th {
    font-weight: normal;
    color: #999;
    padding: .5rem 0;
    cursor: pointer;
    &:hover {
      color: #777;
    }
  }
  td {
    color: #5a9cb6;
    padding: 1rem 0;
  }
  tbody tr:hover {
    background: #f1f1f1;
  }
}
table th, table td {
  text-align: left;
}
</style>
