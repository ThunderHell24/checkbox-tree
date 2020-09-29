<template>
    <div class="checboxTree">
        <Rule
            v-for="rule of rights"
            v-bind:rule="rule"
            v-bind:key="rule.id"
            v-bind:rights="rights"
            v-on:change-parent="changeParent"
        />
    </div>
</template>

<script>
import Rule from '@/components/Rule'
export default {
    props: ['rights'],
    components: {
        Rule,
    },
    methods: {
        changeParent(rule) {
            rule.checked = !rule.checked
            const parent = this.rights.find(
                (parent) => parent.id == rule.parentID
            )
            const neighbours = this.rights.filter(
                (neighbour) => neighbour.parentID == rule.parentID
            )
            function isTrue(item) {
                return item == true
            }
            function isFalse(item) {
                return item == false
            }

            const neighboursState = []
            neighbours.forEach((item) => {
                neighboursState.push(item.checked)
            })

            if (rule.hasChild && !rule.checked) {
                rule.checked = false
                rule.children.forEach((item) => {
                    this.rights.forEach((el) => {
                        if (el.id == item) {
                            el.checked = false
                        }
                    })
                })
            } else if (rule.hasChild && rule.checked) {
                rule.checked = true
                rule.children.forEach((item) => {
                    this.rights.forEach((el) => {
                        if (el.id == item) {
                            el.checked = true
                        }
                    })
                })
            } else if (neighboursState.every(isTrue) && rule.checked) {
                parent.checked = true
                parent.indeterminate = false
            } else if (neighboursState.every(isFalse) && !rule.checked) {
                parent.checked = false
                parent.indeterminate = false
            } else if (rule.checked && neighboursState.some(isTrue)) {
                parent.checked = false
                parent.indeterminate = true
            } else if (!rule.checked && neighboursState.some(isTrue)) {
                parent.checked = false
                parent.indeterminate = true
            }
        },
    },
}
</script>

<style lang="scss" scoped>
ul {
    display: flex;
    align-items: start;
    justify-content: flex-start;
    list-style: none;
    padding: 0;
    margin: 2rem 0;
    width: 100%;
}
button {
    width: 150px;
    height: 40px;
    margin: 1rem;
    background-color: #0076ff;
    font-size: 1rem;
    font-weight: bold;
    color: white;
    outline: none;
    cursor: pointer;
    border-radius: 3px;
    border: 0px;
    &:hover {
        background-color: #086bdb;
    }
}
.checboxTree {
    padding: 1rem 0;
}
</style>
