<template>
  <q-page padding>
    <q-table
      title="Data Siswa"
      :data="data"
      :columns="columns"
      row-key="nomor_induk"
    >
      <template v-slot:top-right>
        <q-btn
          icon="add_box"
          label="Input Data Siswa"
          unelevated
          color="primary"
          :to="{ name: 'inputSiswa' }"
        />
      </template>
      <template v-slot:body="props">
        <q-tr :props="props">
          <q-td key="nomor_induk" :props="props">
            {{ props.row.nomor_induk }}
          </q-td>
          <q-td key="nama_lengkap" :props="props">
            {{ props.row.nama_lengkap }}
          </q-td>
          <q-td key="kelas" :props="props">
            {{ props.row.kelas }}
          </q-td>
          <q-td key="jurusan" :props="props">
            {{ props.row.jurusan }}
          </q-td>
          <q-td key="tahun_pelajaran" :props="props">
            {{ props.row.tahun_pelajaran }}
          </q-td>
          <q-td key="mapel" :props="props">
            {{ props.row.mapel }}
          </q-td>
          <q-td key="semester" :props="props">
            {{ props.row.semester }}
          </q-td>
          <q-td key="nilai" :props="props">
            {{ props.row.nilai }}
          </q-td>
          <q-td key="aksi" :props="props">
            <q-btn
              label="Edit"
              icon="edit"
              :to="{ name: 'editSiswa', params: { id: props.row._id }}"
              color="warning"
              unelevated
            />
            <q-btn
              label="Hapus"
              icon="edit"
              color="negative"
              @click="confirm(props.row._id)"
              class="q-ml-md"
              unelevated
            />
          </q-td>
        </q-tr>
      </template>
    </q-table>
  </q-page>
</template>
<script>

export default {
  data () {
    return {
      columns: [
        {
          name: 'nomor_induk',
          align: 'left',
          label: 'Nomor Induk',
          field: 'nomor_induk'
        },
        {
          name: 'nama_lengkap',
          align: 'left',
          label: 'Nama Lengkap',
          field: 'nama_lengkap'
        },
        {
          name: 'kelas',
          align: 'left',
          label: 'Kelas',
          field: 'kelas'
        },
        {
          name: 'jurusan',
          align: 'left',
          label: 'Jurusan',
          field: 'jurusan'
        },
        {
          name: 'tahun_pelajaran',
          align: 'left',
          label: 'Tahun Pelajaran',
          field: 'tahun_pelajaran'
        },
        {
          name: 'mapel',
          align: 'left',
          label: 'Mata Pelajaran',
          field: 'mapel'
        },
        {
          name: 'semester',
          align: 'left',
          label: 'Semester',
          field: 'semester'
        },
        {
          name: 'nilai',
          align: 'left',
          label: 'Nilai',
          field: 'nilai'
        },
        {
          name: 'aksi',
          align: 'left',
          label: 'Aksi',
          field: 'aksi'
        }
      ],
      data: []
    }
  },
  created () {
    this.getData()
  },
  methods: {
    getData () {
      this.$axios.get('siswa/getAll')
        .then(res => {
          this.data = res.data.result
        })
    },
    confirm (id) {
      this.$q.dialog({
        title: 'Konfirmasi',
        message: 'Apakah Anda Yakin ?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.$axios.put(`siswa/delete/${id}`)
          .then(res => {
            if (res.data.status) {
              this.$q.notify({
                message: res.data.pesan,
                color: 'positive'
              })
              this.getData()
            } else {
              this.$q.notify({
                message: res.data.pesan,
                color: 'negative'
              })
            }
          })
      })
    }
  }
}
</script>
