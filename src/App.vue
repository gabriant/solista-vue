<template>
  <div id="app" class="container">
    <TheNavbar></TheNavbar>

    <div id="app-content">
      <div class="card">
        <div class="card-body p-5">
          <h2 class="card-title">Donec nec justo eget felis facilisis fermentum.</h2>
          <div class="card-description">
            Morbi in sem quis dui placerat ornare. Pellentesque odio nisi, euismod in, pharetra a, ultricies in, diam. Sed arcu. Cras consequat.
          </div>
          <div class="mt-5">
            <ul class="list-group">
              <li class="list-group-item">Cras justo odio</li>
              <li class="list-group-item">Dapibus ac facilisis in</li>
              <li class="list-group-item">Morbi leo risus</li>
              <li class="list-group-item">Porta ac consectetur ac</li>
              <li class="list-group-item">Vestibulum at eros</li>
              <li class="list-group-item">Cras justo odio</li>
              <li class="list-group-item">Dapibus ac facilisis in</li>
              <li class="list-group-item">Morbi leo risus</li>
              <li class="list-group-item">Porta ac consectetur ac</li>
              <li class="list-group-item">Vestibulum at eros</li>
              <li class="list-group-item">Cras justo odio</li>
              <li class="list-group-item">Dapibus ac facilisis in</li>
              <li class="list-group-item">Morbi leo risus</li>
              <li class="list-group-item">Porta ac consectetur ac</li>
              <li class="list-group-item">Vestibulum at eros</li>
              <li class="list-group-item">Cras justo odio</li>
              <li class="list-group-item">Dapibus ac facilisis in</li>
              <li class="list-group-item">Morbi leo risus</li>
              <li class="list-group-item">Porta ac consectetur ac</li>
              <li class="list-group-item">Vestibulum at eros</li>
            </ul>
          </div>
        </div>
      </div>
    </div>

    <TheFooter></TheFooter>

  </div>
</template>

<script>
import Vue from 'vue'
import TheFooter from './components/TheFooter'
import TheNavbar from './components/TheNavbar'

export default Vue.extend({
  name: 'app',
  components: {
    TheFooter, TheNavbar
  },

  data () { return {
    item: null,
    items: [
      { name: 'Cras justo odio', done: false },
      { name: 'Dapibus ac facilisis in', done: false },
      { name: 'Morbi leo risus', done: true },
      { name: 'Porta ac consectetur ac', done: false },
      { name: 'Vestibulum at eros', done: false }
    ]
  }},

  methods: {
    doAddItem () {
      this.items.push({
        name: this.item,
        done: false
      })
      this.item = null
    },

    doClear () {
      this.items.forEach(el => el.done = false)
    },
  }

});
</script>
