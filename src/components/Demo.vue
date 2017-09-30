<template>
    <div class="demo">
        <div class="container">
            <div class="row">
                <div class="col-md-12">
                    <button class="btn btn-primary" :disabled="isLastPage" @click="nextPage">nextPage</button>

                    <table class="table">
                        <thead>
                            <tr>
                                <th v-for="col in columns" :key="col.label">{{col.label}}</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="row in currentData" :key="row.id">
                                <!-- <td>{{row.title}}</td> -->
                                <td v-for="col in columns" :key="col.label">{{findByCol(row, col)}}</td>
                            </tr>
                        </tbody>
                    </table>

                    <nav aria-label="Page navigation">
                    <ul class="pagination">
                        <li>
                        <a href="#" aria-label="Previous">
                            <span aria-hidden="true">&laquo;</span>
                        </a>
                        </li>
                        <li><a href="#">1</a></li>
                        <li><a href="#">2</a></li>
                        <li><a href="#">3</a></li>
                        <li><a href="#">4</a></li>
                        <li><a href="#">5</a></li>
                        <li>
                        <a href="#" aria-label="Next">
                            <span aria-hidden="true">&raquo;</span>
                        </a>
                        </li>
                    </ul>
                    </nav>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import _ from 'lodash'
import axios from 'axios'

export default {
    data() {
        return {
            columns: [{ label: 'ID', field: 'id' }, { label: '标题', field: 'title' }, { label: '内容', field: 'body' }],
            searchObject: null,
            pageObject: {
                index: 1,
                count: 10,
                totalPage: 1
            },
            currentData: null
        }
    },
    watch: {
        searchObject() {
            updateData(this.searchObject, this.pageObject)
        },
        'pageObject.index'(newPageObj) {
            this.updateData(this.searchObject, this.pageObject)
        },
        // pageObject: {
        //     handler(newPageObj) {
        //         console.log('update data ', newPageObj);
        //         this.updateData(this.searchObject, this.pageObject)
        //     },
        //     deep: true
        // }
    },
    computed: {
        isFirstPage() {
            return this.pageObject.index === 1
        },
        isLastPage() {
            return this.pageObject.index === this.pageObject.totalPage
        }
    },
    methods: {
        findByCol(row, col) {
            return row[col.field]
        },
        updateData(searchObject, pageObject) {
            axios.get('http://jsonplaceholder.typicode.com/posts', {
                params: {
                    _page: pageObject.index,
                    _limit: pageObject.count
                }
            }).then(response => {
                var total = parseInt(response.headers['x-total-count']);
                console.log(total)
                this.pageObject.totalPage = Math.ceil(total / this.pageObject.count) 
                this.currentData = response.data
            })
        },
        nextPage() {
            this.pageObject.index += 1
        }
    },
    created() {
        this.updateData(this.searchObject, this.pageObject)
    }
}
</script>

<style scoped>
/* @import url(https://unpkg.com/purecss@1.0.0/build/pure-min.css); */
</style>
