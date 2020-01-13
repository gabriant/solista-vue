<template>
  <div id="app" class="container">
    <TheNavbar></TheNavbar>

    <div id="app-content">
      <div class="card">
        <div class="card-body p-5">

          <input
            v-model="list.title"
            type="text"
            maxlength="50"
            class="form-control custom-input card-title"
          >

          <textarea
            v-model="list.description"
            maxlength="200"
            rows="2"
            class="form-control custom-input card-description"
          ></textarea>

          <div class="mt-3">
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

const STORAGE_ATTRIBUTE = 'solistalist'

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
    this.doInitList()
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

    doInitList () {
      let exists = this.doGetList()
      if (!exists || !exists.title) {
        exists = defaultList
        this.doSaveList(exists)
      }
      this.list = exists
    },

    doGetList:() => JSON.parse(localStorage.getItem(STORAGE_ATTRIBUTE)),
    doSaveList: (json) => localStorage.setItem(STORAGE_ATTRIBUTE, JSON.stringify(json))
  }

});
</script>
