<template>
  <div class="q-pa-md" style="max-width: 400px">

    <q-form
      @submit="onSubmit"
      class="q-gutter-md"
    >
      <q-input
        filled
        v-model="form.nomor_induk"
        label="Nomor Induk Siswa *"
        :rules="[ val => val && val.length > 0 || 'Mohon Isi Nomor Induk']"
      />
      <q-input
        filled
        v-model="form.nama_lengkap"
        label="Nama lengkap *"
        :rules="[ val => val && val.length > 0 || 'Mohon Isi Nama Lengkap']"
      />
      <q-input
        filled
        v-model="form.kelas"
        label="Kelas *"
        :rules="[ val => val && val.length > 0 || 'Mohon Isi Kelas']"
      />
      <q-input
        filled
        v-model="form.jurusan"
        label="Jurusan *"
        :rules="[ val => val && val.length > 0 || 'Mohon Isi Jurusan']"
      />
      <q-input
        filled
        v-model="form.tahun_pelajaran"
        label="Tahun Pelajaran *"
        :rules="[ val => val && val.length > 0 || 'Mohon Isi Tahun Pelajaran']"
      />
      <q-input
        filled
        v-model="form.mapel"
        label="Mata Pelajaran *"
        :rules="[ val => val && val.length > 0 || 'Mohon Isi Mata Pelajaran']"
      />
      <q-input
        filled
        v-model="form.semester"
        label="Semester *"
        :rules="[ val => val && val.length > 0 || 'Mohon Isi Semester']"
      />
      <q-input
        filled
        v-model="form.nilai"
        label="Nilai *"
        :rules="[ val => val && val.length > 0 || 'Mohon Isi Nilai']"
      />

      <div>
        <q-btn label="Submit" type="submit" color="primary"/>
      </div>
    </q-form>

  </div>
</template>
<script>

export default {
  data () {
    return {
      form: {
        nomor_induk: null,
        nama_lengkap: null,
        kelas: null,
        jurusan: null,
        tahun_pelajaran: null,
        mapel: null,
        semester: null,
        nilai: null
      }
    }
  },
  methods: {
    onSubmit () {
      this.$axios.post('siswa/insert', this.form)
        .then(res => {
          if (res.data.status) {
            this.$q.notify({
              message: res.data.pesan,
              color: 'positive'
            })
            this.$router.push({ name: 'dashboard' })
          } else {
            this.$q.notify({
              message: res.data.pesan,
              color: 'negative'
            })
          }
        })
    }
  }
}
</script>
