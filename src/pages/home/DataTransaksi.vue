<template>
  <q-page>
    <div class="q-pa-md">
      <q-table
        title="Treats"
        :data="data"
        :columns="columns"
        row-key="id"
        :filter="filter"
        :loading="loading"
      >

        <template v-slot:top>
          <span class="text-h5 text-weight-light q-pa-md">
        <span class="text-blue-grey-14">Data Transaksi</span>
      </span>
          <q-space />
          <q-input borderless dense debounce="300" color="primary" v-model="filter">
            <template v-slot:append>
              <q-icon name="search" />
            </template>
          </q-input>
        </template>

      </q-table>
    </div>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      loading: false,
      filter: '',
      rowCount: 10,
      columns: [
        {
          name: 'desc',
          required: true,
          label: 'Kode Transaksi',
          align: 'left',
          field: row => row.kodetransaksi,
          format: val => `${val}`,
          sortable: true
        },
        { name: 'Kodetransaksi', align: 'center', label: 'Kode Transaksi', field: 'kodetransaksi', sortable: true },
        { name: 'NamaPembli', align: 'center', label: 'Nama Pembeli', field: 'namapembeli', sortable: true },
        { name: 'JudulBuku', align: 'center', label: 'Judul Buku', field: 'JudulBuku' },
        { name: 'HargaBuku', align: 'center', label: 'Harga Buku', field: 'hargabuku' },
        { name: 'JumblahBeli', align: 'center', label: 'Jumblah Beli', field: 'jumblahbeli' },
        { name: 'Total', align: 'center', label: 'Total', field: 'total' }

      ],
      data: [
        {
          kodetransaksi: 'Trans-001',
          namapembeli: 'John Petrucci',
          JudulBuku: 'Pemograman 3',
          hargabuku: '250000',
          jumblahbeli: '2',
          total: '500000'

        },
        {
          kodetransaksi: 'Trans-002',
          namapembeli: 'Yngwie Maimstream',
          JudulBuku: 'Pemograman 3',
          hargabuku: '250000',
          jumblahbeli: '1',
          total: '2500000'

        },
        {
          kodetransaksi: 'Trans-003',
          namapembeli: 'Slash',
          JudulBuku: 'Prak Pemograman 3',
          hargabuku: '350000',
          jumblahbeli: '3',
          total: '1050000'

        }
      ]
    }
  },

  methods: {
    // emulate fetching data from server
    addRow () {
      this.loading = true
      setTimeout(() => {
        const
          index = Math.floor(Math.random() * (this.data.length + 1)),
          row = this.original[Math.floor(Math.random() * this.original.length)]
        if (this.data.length === 0) {
          this.rowCount = 0
        }
        row.id = ++this.rowCount
        const addRow = { ...row } // extend({}, row, { name: `${row.name} (${row.__count})` })
        this.data = [...this.data.slice(0, index), addRow, ...this.data.slice(index)]
        this.loading = false
      }, 500)
    },

    removeRow () {
      this.loading = true
      setTimeout(() => {
        const index = Math.floor(Math.random() * this.data.length)
        this.data = [...this.data.slice(0, index), ...this.data.slice(index + 1)]
        this.loading = false
      }, 500)
    }
  }
}
</script>
