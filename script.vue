const app = new Vue({
  el: '#app',
  data: {
    lens: [],
    newLens: null
  },
  mounted() {
    if (localStorage.getItem('lens')) {
      try {
        this.lens = JSON.parse(localStorage.getItem('lens'));
      } catch(e) {
        localStorage.removeItem('lens');
      }
    }
  },
  methods: {
    addLens() {
      // ensure they actually typed something
      if (!this.newLens) {
        return;
      }

      this.lens.push(this.newLens);
      this.newLens = '';
      this.saveLens();
    },
    removeLens(x) {
      this.lens.splice(x, 1);
      this.saveLens();
    },
    saveLenses() {
      const parsed = JSON.stringify(this.lens);
      localStorage.setItem('lens', parsed);
    }
  }
})
