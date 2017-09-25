<template>
  <div class="hello">
    <div class="container">
      <div class="row">
        <div class="col-md-4">
          <div class="list-group">
            <a @click.prevent="clickCategory(item)" class="list-group-item" :class="{active: item===selectedCatagory}" v-for="item in categories" :key="item.id">{{item.title}}</a>
          </div>
        </div>
        <div class="col-md-4">
          <div class="input-group" style="margin-bottom: 5px;">
            <input type="text" class="form-control" placeholder="Search for...">
            <span class="input-group-btn">
              <button class="btn btn-default" type="button">GO</button>
            </span>
          </div>
          <!-- /input-group -->
          <div class="list-group">
            <a @click.prevent="clickTarget(item)" :class="{active: item===selectedTarget}" class="list-group-item" v-for="item in targetList" :key="item.id">{{item.ip}}</a>
          </div>
          <nav aria-label="...">
            <ul class="pager">
              <li>
                <a href="#">Previous</a>
              </li>
              <li>
                <a href="#">Next</a>
              </li>
            </ul>
          </nav>
        </div>
        <div class="col-md-4">
          <div class="list-group">
            <a v-for="item in indexList" :key="item.id" :class="{active: item===selectedIndex}" @click.prevent="clickIndex(item)" class="list-group-item">{{item.title}}</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
  name: 'hello',
  data() {
    return {
      categories: [{ id: 1, title: '主机' }, { id: 2, title: '服务器' }, { id: 3, title: '组件' }],
      selectedCatagory: '',
      selectedTarget: '',
      selectedIndex: ''
    }
  },
  computed: {
    targetList() {
      if (this.selectedCatagory) {
        var arr = _.map(_.range(10), (idx) => { return { ip: this.selectedCatagory.title + ' ' + idx, id: idx } })
        console.log(arr);
        return arr
      } else {
        return undefined
      }
    },
    indexList() {
      if (this.selectedTarget) {
        var arr = _.map(_.range(10), (idx) => { return { title: this.selectedTarget.ip + '指标' + idx, id: idx } })
        console.log(arr);
        return arr
      } else {
        return undefined
      }
    }
  },
  methods: {
    clickCategory(item) {
      this.selectedCatagory = item
    },
    clickTarget(target) {
      this.selectedTarget = target
    },
    clickIndex(index) {
      this.selectedIndex = index
      console.log(_.join([this.selectedCatagory.title, this.selectedTarget.ip, this.selectedIndex.title], ', '));
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
@import url('../../node_modules/bootstrap/dist/css/bootstrap.css');
</style>
