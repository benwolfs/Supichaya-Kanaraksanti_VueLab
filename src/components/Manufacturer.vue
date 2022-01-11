<template>
  <div class="grid grid-cols-2 gap-4 border-black">
    <div class="ml-10 mr-0">
      <h1 class="font-black mb-3">Manufacturer</h1>
      <ul v-for="m in manufacturer" :key="m.id" class="border border-black">
        <li>
          <button @click="changeManufacturerId(m.id)">
            <img :src="m.Logo" width="100" />
          </button>
        </li>
      </ul>
    </div>
    <div>
      <slot :factId="currentManufactId"></slot>
    </div>
  </div>
</template>
<script>
import axios from 'axios';

export default {
  name: 'Manufacturer',
  data() {
    return {
      currentManufactId: 0,
      manufacturer: [
        { id: 1, Title: 'Asus' },
        { id: 2, Title: 'Dell' },
      ],
    };
  },
  methods: {
    async getManufacturer() {
      axios.get('https://demo.yume-dev.me/manufacturers').then((res) => {
        console.log('Manfact: ', res.data);
        this.manufacturer = res.data;
      });
      // const res = await axios.get('https://demo.yume-dev.me/manufacturers');
      // console.log(res);
    },
    changeManufacturerId(id) {
      this.currentManufactId = id;
      // console.log(`ID : ${id}`);
    },
  },
  created() {
    this.getManufacturer();
  },
};
</script>
