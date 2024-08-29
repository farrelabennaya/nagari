<template>
  <div>
    <AppHeader />
    <div class="flex overflow-hidden bg-white pt-16">
      <SidebarAdmin />
      <div
        id="main-content"
        class="h-full w-full bg-gray-50 relative overflow-y-auto sm:ml-64"
      >
        <div class="custom-header to-gray-100 p-6 pb-32 pt-5">
          <main>
            <div
              class="bg-white rounded-lg shadow-sm p-6 flex justify-between items-center relative overflow-x-auto ml-5 mr-5 mt-5 mb-5"
            >
              <div>
                <h2 class="text-xl font-bold text-gray-800">
                  Anggota Keluarga
                </h2>
                <p class="text-gray-500">Tambah Anggota Keluarga</p>
              </div>
            </div>
          </main>
        </div>
        <form
          @submit.prevent="createAnggotaKeluarga"
          class="grid grid-cols-1 xl:grid-cols-1 gap-4 px-11 pt-6 dark:bg-gray-900 -mt-20"
         >
          <!-- Column 1: Jumlah KK and Alamat -->

          <!-- Column 2: Buat Kepala Keluarga -->
          <div class="">
            <div
              class="p-4 mb-4 bg-white border border-gray-200 rounded-lg shadow-sm dark:border-gray-700 sm:p-6 dark:bg-gray-800"
             >
              <h3 class="mb-4 text-xl font-semibold dark:text-white">
                Buat Anggota Keluarga
              </h3>
              <div class="grid grid-cols-2 gap-6">
                <div>
                  <label
                    for="nama"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Nama</label
                  >
                  <input
                    id="nama"
                    v-model="form.nama"
                    type="text"
                    placeholder="Nama"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                  />
                  <span v-if="errors.nama" class="text-red-500">
                    {{ errors.nama[0] }}
                  </span>
                </div>

                <div>
                  <label
                    for="nik"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >NIK</label
                  >
                  <input
                    id="nik"
                    v-model="form.nik"
                    type="text"
                    maxlength="16"
                    @input="validateNik"
                    placeholder="NIK (16 Digit)"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                  />
                  <span v-if="errors.nik" class="text-red-500">
                    {{ errors.nik[0] }}
                  </span>
                </div>

                <div>
                  <label
                    for="tempat_lahir"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Tempat Lahir</label
                  >
                  <input
                    id="tempat_lahir"
                    v-model="form.tempat_lahir"
                    type="text"
                    placeholder="Tempat Lahir"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                  />
                  <span v-if="errors.tempat_lahir" class="text-red-500">
                    {{ errors.tempat_lahir[0] }}
                  </span>
                </div>

                <div>
                  <label
                    for="tanggal_lahir"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Tanggal Lahir</label
                  >
                  <input
                    id="tanggal_lahir"
                    v-model="form.tanggal_lahir"
                    type="date"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                  />
                  <span v-if="errors.tanggal_lahir" class="text-red-500">
                    {{ errors.tanggal_lahir[0] }}
                  </span>
                </div>

                <div>
                  <label
                    for="agama"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Agama</label
                  >
                  <select
                    id="agama"
                    v-model="form.agama"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                  >
                    <option disabled value="">Pilih Agama</option>
                    <option
                      v-for="agama in agamaOptions"
                      :key="agama"
                      :value="agama"
                    >
                      {{ agama }}
                    </option>
                  </select>
                  <span v-if="errors.agama" class="text-red-500">
                    {{ errors.agama[0] }}
                  </span>
                </div>

                <div>
                  <label
                    for="jenis_kelamin"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Jenis Kelamin</label
                  >
                  <select
                    id="jenis_kelamin"
                    v-model="form.jenis_kelamin"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                  >
                    <option disabled value="">Pilih Jenis Kelamin</option>
                    <option
                      v-for="jenis in jenisKelaminOptions"
                      :key="jenis"
                      :value="jenis"
                    >
                      {{ jenis }}
                    </option>
                  </select>
                  <span v-if="errors.jenis_kelamin" class="text-red-500">
                    {{ errors.jenis_kelamin[0] }}
                  </span>
                </div>

                <div>
                  <label
                    for="pendidikan"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Pendidikan</label
                  >
                  <select
                    id="pendidikan"
                    v-model="form.pendidikan"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                  >
                    <option disabled value="">Pilih Pendidikan</option>
                    <option
                      v-for="pendidikan in pendidikanOptions"
                      :key="pendidikan"
                      :value="pendidikan"
                    >
                      {{ pendidikan }}
                    </option>
                  </select>
                  <span v-if="errors.pendidikan" class="text-red-500">
                    {{ errors.pendidikan[0] }}
                  </span>
                </div>

                <div>
                  <label
                    for="pekerjaan"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Pekerjaan</label
                  >
                  <select
                    id="pekerjaan"
                    v-model="form.pekerjaan"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                  >
                    <option disabled value="">Pilih Pekerjaan</option>
                    <option
                      v-for="pekerjaan in pekerjaanOptions"
                      :key="pekerjaan"
                      :value="pekerjaan"
                    >
                      {{ pekerjaan }}
                    </option>
                  </select>
                  <span v-if="errors.pekerjaan" class="text-red-500">
                    {{ errors.pekerjaan[0] }}
                  </span>
                </div>

                <div>
                  <label
                    for="nama_ayah"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Nama Ayah</label
                  >
                  <input
                    id="nama_ayah"
                    type="text"
                    placeholder="Nama Ayah"
                    v-model="form.nama_ayah"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                  />
                  <span
                    v-if="errors.nama_ayah"
                    class="text-red-500"
                    >{{ errors.nama_ayah[0] }}</span
                  >
                </div>

                <div>
                  <label
                    for="nama_ibu"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Nama Ibu</label
                  >
                  <input
                    id="nama_ibu"
                    type="text"
                    placeholder="Nama Ibu"
                    v-model="form.nama_ibu"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                  />
                  <span
                    v-if="errors.nama_ibu"
                    class="text-red-500"
                    >{{ errors.nama_ibu[0] }}</span
                  >
                </div>

                <div>
                  <label
                    for="status_perkawinan"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Status Perkawinan</label
                  >
                  <select
                    id="status_perkawinan"
                    v-model="form.status_perkawinan"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                  >
                    <option disabled value="">Pilih Status Perkawinan</option>
                    <option
                      v-for="status in statusPerkawinanOptions"
                      :key="status"
                      :value="status"
                    >
                      {{ status }}
                    </option>
                  </select>
                  <span v-if="errors.status_perkawinan" class="text-red-500">
                    {{ errors.status_perkawinan[0] }}
                  </span>
                </div>

                <div>
                  <label
                    for="status_perkawinan"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Hubungan Keluarga</label
                  >
                  <select
                    id="hubungan_keluarga"
                    v-model="form.hubungan_keluarga"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                  >
                    <option disabled value="">Pilih Hubungan Keluarga</option>
                    <option
                      v-for="hubungan in hubunganKeluargaOptions"
                      :key="hubungan"
                      :value="hubungan"
                    >
                      {{ hubungan }}
                    </option>
                  </select>
                  <span v-if="errors.hubungan_keluarga" class="text-red-500">
                    {{ errors.hubungan_keluarga[0] }}
                  </span>
                </div>
              </div>

              <div class="mt-6">
                <button
                  type="button"
                  @click="cancelCreate"
                  class="mr-2 bg-gray-500 text-white font-medium rounded-lg px-4 py-2 hover:bg-gray-600 focus:outline-none focus:ring-2 focus:ring-gray-300"
                >
                  Batal
                </button>
                <button
                  type="submit"
                  class="bg-blue-500 text-white font-medium rounded-lg px-4 py-2 hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-blue-300"
                >
                  Simpan
                </button>
              </div>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, reactive } from "vue";
import AppHeader from "~/components/AppHeader.vue";
import SidebarAdmin from "~/components/SidebarAdmin.vue";
import { useRouter } from "vue-router";

definePageMeta({
  middleware: ["auth", "role"],
  colorMode: "light",
});

export default {
  components: {
    AppHeader,
    SidebarAdmin,
  },
  setup() {
    const router = useRouter();
    const form = reactive({
      nama: "",
      nik: "",
      tempat_lahir: "",
      tanggal_lahir: "",
      agama: "",
      jenis_kelamin: "",
      pendidikan: "",
      pekerjaan: "",
      status_perkawinan: "",
      hubungan_keluarga: "",
      keluarga_id: router.currentRoute.value.query.keluarga_id,
      kepala_keluarga_id: router.currentRoute.value.query.kepala_keluarga_id, // Pastikan ini di-set
    });

    const errors = reactive({});
    // Function to validate NIK input (only allow numbers, check length)
    const validateNik = (e) => {
      const input = e.target.value.replace(/\D/g, ""); // Allow only digits

      if (input.length < 16) {
        errors.nik = ["NIK harus terdiri dari 16 digit"];
      } else if (input.length > 16) {
        errors.nik = ["NIK tidak boleh lebih dari 16 digit"];
      } else {
        errors.nik = null; // No error
      }

      // Update the form data with validated input
      form.nik = input;
    };

    const notification = reactive({
      show: false,
      message: "",
    });

    const agamaOptions = [
      "Islam",
      "Kristen",
      "Katolik",
      "Hindu",
      "Buddha",
      "Khonghucu",
    ];

    const jenisKelaminOptions = ["Laki-laki", "Perempuan"];

    const pendidikanOptions = [
      "TIDAK / BELUM SEKOLAH",
      "TAMAT SD / SEDERAJAT",
      "SLTA / SEDERAJAT",
      "SLTP/SEDERAJAT",
      "BELUM TAMAT SD/SEDERAJAT",
      "DIPLOMA IV/ STRATA I",
      "DIPLOMA I / II",
      "AKADEMI/ DIPLOMA III/S. MUDA",
      "STRATA II",
      "STRATA III",
    ];

    const pekerjaanOptions = [
      "Belum Ditentukan",
      "Belum/Tidak Bekerja",
      "Pelajar/Mahasiswa",
      "Mengurus Rumah Tangga",
      "Buruh Harian Lepas",
      "Buruh Peternakan",
      "Buruh Tani/Perkebunan",
      "Guru",
      "Tentara Nasional Indonesia (TNI)",
      "Kepolisian RI (POLRI)",
      "Karyawan BUMD",
      "Karyawan BUMN",
      "Karyawan Honorer",
      "Karyawan Swasta",
      "Mekanik",
      "Pedagang",
      "Pegawai Negeri Sipil (PNS)",
      "Pensiunan",
      "Perancang Busana",
      "Perawat",
      "Perdagangan",
      "Petani/Pekebun",
      "Peternak",
      "Sopir",
      "Tabib",
      "Transportasi",
      "Tukang Batu",
      "Tukang Cukur",
      "Tukang Jahit",
      "Tukang Kayu",
      "Tukang Las/Pandai Besi",
      "Wiraswasta",
    ];

    const statusPerkawinanOptions = [
      "Belum Kawin",
      "Kawin",
      "Cerai Hidup",
      "Cerai Mati",
    ];

    const hubunganKeluargaOptions = [
      "Istri",
      "Anak",
      "Orang Tua",
      "Menantu",
      "Mertua",
      "Cucu",
      "Famili Lain",
      "Lainnya",
    ];

    const showNotification = (message) => {
      notification.message = message;
      notification.show = true;
      setTimeout(() => {
        notification.show = false;
      }, 3000);
    };
    const createAnggotaKeluarga = async () => {

        if (form.nik.length !== 16) {
    errors.nik = ["NIK harus terdiri dari 16 digit"];
    showNotification("NIK harus terdiri dari 16 digit");
    return; // Stop execution if NIK is invalid
  }

      try {
        // Reset previous errors
        Object.keys(errors).forEach((key) => {
          errors[key] = null;
        });

        const response = await fetch(
          "https://www.demo-ta.my.id/api/anggota_keluargas",
          {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
              Accept: "application/json",
            },
            body: JSON.stringify(form),
          }
        );

        if (!response.ok) {
          const errorData = await response.json();

          // Update errors with the response from the server
          Object.keys(errorData.errors).forEach((key) => {
            errors[key] = errorData.errors[key];
          });

          return; // Stop further execution if there are errors
        }

        const newAnggota = await response.json();
        showNotification("Anggota Keluarga berhasil ditambahkan!");
        cancelCreate(); // Navigate back or reset the form
      } catch (error) {
        console.error("Gagal menambahkan anggota keluarga:", error);
        showNotification("Gagal menambahkan anggota keluarga");
      }
    };
    const cancelCreate = () => {
      router.push({
        path: "/admin/nagari/keluarga/keluargaDetail",
        query: { id: form.keluarga_id },
      });
    };

    return {
      form,
      errors,
      createAnggotaKeluarga,
      showNotification,
      cancelCreate,
      agamaOptions,
      jenisKelaminOptions,
      pendidikanOptions,
      pekerjaanOptions,
      validateNik,
      statusPerkawinanOptions,
      hubunganKeluargaOptions,
    };
  },
};
</script>
<style scoped>
.custom-bg-main {
  background-color: #f9fafb;
}

.custom-header {
  background-color: #adc4ce;
}
</style>
