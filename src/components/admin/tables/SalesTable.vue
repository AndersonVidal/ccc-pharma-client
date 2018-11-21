<template>
  <div>
    <items-table :titles="headTable" :data="vendas"/>
  </div>
</template>

<script>
import ItemsTable from '@/components/admin/ItemsTable'

export default {
  name: 'SalesTable',
  data () {
    return {
      headTable: [
        {label: 'Id', property: 'id'},
        {label: 'Data', property: 'data'},
        {label: 'CPF', property: 'cpfCliente'},
        {label: 'Quant. Itens', property: 'quantidadeItens'},
        {label: 'Total (R$)', property: 'valorTotal'}
      ],
      vendas: [
        {
          id: 1,
          data: '20/10/2018',
          cpfCliente: '111.111.111-11',
          quantidadeItens: 2,
          valorTotal: 30
        },
        {
          id: 2,
          data: '20/10/2018',
          cpfCliente: '121.121.121-12',
          quantidadeItens: 4,
          valorTotal: 120
        },
        {
          id: 3,
          data: '18/10/2018',
          cpfCliente: '113.113.113-13',
          quantidadeItens: 1,
          valorTotal: 45
        },

        {
          id: 4,
          data: '21/10/2018',
          cpfCliente: '411.411.411-41',
          quantidadeItens: 6,
          valorTotal: 23
        }
      ]
    }
  },
  components: {
    ItemsTable
  },
}
</script>

