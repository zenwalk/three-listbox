<template>
  <div class="hello">
    <div class="container">
      <div class="row">
        <div class="col-md-4 col-md-offset-4">
          <div @click="selectCatagory" class="list-group">
            <a href="#" class="list-group-item active">Cras justo odio</a>
            <a href="#" class="list-group-item">Dapibus ac facilisis in</a>
            <a href="#" class="list-group-item">Morbi leo risus</a>
            <a href="#" class="list-group-item">Porta ac consectetur ac</a>
            <a href="#" class="list-group-item">Vestibulum at eros</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      selectedCatagory: '',
      msg: 'Welcome to Your Vue.js PWA'
    }
  },
  methods: {
    foo() {
      return
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
@import url('../../node_modules/bootstrap/dist/css/bootstrap.css');
</style>
