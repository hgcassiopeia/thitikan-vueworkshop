<template>
  <h1 class="font-black mb-3">Devices</h1>
  <div class="grid grid-cols-3 gap-4 border border-black ml-0 mr-5 p-3">
    <ul v-for="d in devices" :key="d.id" class="border border-black">
      <li>
        <router-link :to="{ name: 'device', params: { id: d.id } }">
          <img :src="d.Photo" />
        </router-link>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Devices',
  props: {
    manufacturerId: Number,
  },
  data() {
    return {
      devices: [
        { id: 1, DeviceName: 'Dell X13' },
        { id: 2, DeviceName: 'Asus ROG' },
      ],
    };
  },
  watch: {
    manufacturerId: function (newId, oldId) {
      this.validateId(newId);
    },
  },
  created() {
    this.validateId(0);
  },
  methods: {
    validateId(id) {
      let uri = 'https://demo.yume-dev.me/devices';

      if (id != 0 || id) {
        uri = `${uri}?ManufacturerID=${id}`;
        this.getDevices(uri);
      } else {
        this.getDevices(uri);
      }
    },
    getDevices(uri) {
      axios.get(uri).then((res) => {
        this.devices = res.data;
      });
    },
  },
};
</script>
