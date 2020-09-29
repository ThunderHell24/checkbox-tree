<template>
    <div class="wrapper">
        <h1>Что будем редактировать?</h1>
        <hr />
        <RightsList v-bind:rights="NestedItems()" v-on:selfx="NestedItems" />
    </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component'
import RightsList from '@/components/RightsList.vue'

@Options({
    components: {
        RightsList,
    },
    data() {
        return {
            rights: [
                {
                    id: 1,
                    parentID: 0,
                    name: 'Редактировать что-то одно',
                    checked: false,
                },
                {
                    id: 2,
                    parentID: 1,
                    name: 'Редактировать что-то другое',
                    checked: false,
                },
                {
                    id: 3,
                    parentID: 1,
                    name: 'Редактировать что-то совсем другое',
                    checked: false,
                },
                {
                    id: 4,
                    parentID: 1,
                    name: 'Редактировать что-то или нет?',
                    checked: false,
                },
                {
                    id: 5,
                    parentID: 2,
                    name: 'Редактировать что-то странное',
                    checked: false,
                },
                {
                    id: 6,
                    parentID: 3,
                    name: 'Редактировать что-то иное',
                    checked: false,
                },
                {
                    id: 7,
                    parentID: 3,
                    name: 'Редактировать что-то зелёное',
                    checked: false,
                },
                {
                    id: 8,
                    parentID: 4,
                    name: 'Редактировать что-то иное',
                    checked: false,
                },
                {
                    id: 9,
                    parentID: 4,
                    name: 'Редактировать что-то новое',
                    checked: false,
                },
                {
                    id: 10,
                    parentID: 4,
                    name: 'Редактировать что-то старое',
                    checked: false,
                },
            ],
        }
    },
    methods: {
        NestedItems() {
            const obj: any = this.rights
            const parentsIDs: any = []

            obj.forEach((el: any) => {
                parentsIDs.push(el.parentID)
            })
            obj.forEach((el: any) => {
                const arrChildren: any = []
                obj.map(function(item: any) {
                    if (item.parentID == el.id) {
                        arrChildren.push(item.id)
                    } else {
                        return
                    }
                })
                el.children = arrChildren
                el.indeterminate = false
                if (arrChildren.length > 0) {
                    el.hasChild = true
                } else {
                    el.hasChild = false
                }
            })
            const branch: any = []
            function treeSort(object: any) {
                object.forEach((item: any) => {
                    if (item.hasChild) {
                        branch.push(item)
                        const cond: any = branch.some(function(e: any) {
                            return e.parentID === item.parentID
                        })
                        object.forEach((el: any) => {
                            if (
                                el.parentID === item.id &&
                                el.hasChild == false
                            ) {
                                branch.push(el)
                            }
                        })
                    }
                })
            }
            treeSort(obj)
            return branch
        },
    },
    beforeMount() {
        this.NestedItems()
    },
})
export default class App extends Vue {}
</script>

<style lang="scss">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    // text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0 auto;
    padding: 0;
    text-align: center;
    max-width: 600px;
}
.wrapper {
    width: 100%;
    hr {
        height: 1px;
        background-color: gray;
        border: none;
        margin: 2rem 0 1rem;
    }
    h1 {
        // text-transform: uppercase;
        font-size: 2rem;
        letter-spacing: 0.1rem;
    }
}
</style>
