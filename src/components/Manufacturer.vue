<template>
  <div class="grid grid-cols-2 gap-4 border-black">
    <div class="ml-10 mr-0">
      <h1>Manufacturer</h1>
      <ul v-for="m in manufacturer" :key="m.id" class="border border-black">
        <li>
          <button @click="changeManufacturerId(m.id)">
            <img :src="m.Logo" width="100" />
          </button>
        </li>
      </ul>
    </div>
    <div>
      <slot :factId="currentManufactID"></slot>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Manufacturer',
  data() {
    return {
      currentManufactID: 0,
      manufacturer: [
        { id: 1, Title: 'Dell' },
        { id: 2, Title: 'Asus' },
      ],
    };
  },
  created() {
    this.getManufacturer();
  },
  methods: {
    async getManufacturer() {
      // axios.get('https://demo.yume-dev.me/manufacturers').then((res) => {
      //   console.log(res);
      //   this.manufacturer = res.data
      // });
      const res = await axios.get('https://demo.yume-dev.me/manufacturers');
      // console.log(res.data);
      this.manufacturer = res.data;
    },

    changeManufacturerId(id) {
      // console.log('changeManufacturerId ::: ', id);
      this.currentManufactID = id;
    },
  },
};
</script>
