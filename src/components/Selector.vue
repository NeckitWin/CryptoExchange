<script>
export default {
  props: {
    setCrypto: {
      type: Function,
      required: true
    }
  },
  data() {
    return {
      current: ''
    }
  },
  methods: {
    selectItem(val) {
      this.setCrypto(val)
      this.current = val
    }
  }

}
</script>

<template>
  <ul>
    <li @click="selectItem('BTC')" :className="current == 'BTC' ? 'active' : ''">Bitcoin</li>
    <li @click="selectItem('ETH')" :class="current == 'ETH' ? 'active' : ''">ETH</li>
    <li @click="selectItem('USDT')" :class="current == 'USDT' ? 'active' : ''">USDT</li>
  </ul>
</template>

<style scoped>
ul {
  list-style-type: none;
  width: 200px;
  padding: 0;
  border-radius: 3px;
  border: 3px solid #000;
}

li{
  display: block;
  background: #1A032D;
  color: #fff;
  padding: 20px 0;
  transition: 0.5s ease;
}

li:hover, li.active {
  background: #24043e;
  cursor: pointer;
  transform: scale(1.05);
}
</style>