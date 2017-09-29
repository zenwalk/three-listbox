<template>
    <div class="demo">
        <div class="container">
            <div class="row">
                <div class="col-md-12">
                    <button @click="nextPage">nextPage</button>

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
            columns: [{ label: '标题', field: 'title' }, { label: '内容', field: 'body' }],
            searchObject: null,
            pageObject: {
                index: 1,
                count: 10,
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
    },
    methods: {
        findByCol(row, col) {
            return row[col.field]
        },
        updateData(searchObject, pageObject) {
            console.log('update data ', pageObject);
            axios.get('http://jsonplaceholder.typicode.com/posts', {
                params: {
                    _page: pageObject.index,
                    _limit: pageObject.count
                }
            }).then(response => {
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
