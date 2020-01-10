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
              <li
                v-for="(item, idx) in list.items"
                :key="idx"
                class="list-group-item"
                :class="{ 'list-group-item-info': item.done }"
              >
                <input v-model="item.done" type="checkbox">
              <span class="ml-4">{{ item.content }}</span></li>
            </ul>
          </div>

          <div class="input-group mt-3">
            <div class="input-group-prepend">
              <button
                @click.prevent="doAddItem()"
                class="btn btn-outline-secondary"
              >+</button>
            </div>
            <input
              v-model="newitem"
              @keyup.enter="doAddItem()"
              type="text"
              class="form-control"
              placeholder=""
            >
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
import defaultList from './default-list.json'

export default Vue.extend({
  name: 'app',
  components: {
    TheFooter, TheNavbar
  },

  data () { return {
    newitem: null,
    list: null
  }},

  created () {
    this.checkIfListExists()
    this.list = this.doGetList()
  },

  updated () {
    this.doSaveList(this.list)
  },

  methods: {
    doAddItem () {
      this.list.items.push({
        content: this.newitem,
        done: false
      })
      console.log(this.newitem);
      this.newitem = null
    },

    doClear () {
      this.list.items.forEach(el => el.done = false)
    },

    checkIfListExists () {
      let exists = this.doGetList()
      if (!exists.title)
        this.doSaveList(defaultList)
    },

    doGetList:() => JSON.parse(localStorage.getItem('solistalist')),
    doSaveList: (json) => localStorage.setItem('solistalist', JSON.stringify(json))
  }

});
</script>
