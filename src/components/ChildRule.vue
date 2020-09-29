<template>
    <li v-for="chld of rch.children" :key="chld">
        {{ rights[chld].name }}
    </li>
</template>

<script>
export default {
    props: {
        rule: {
            type: Object,
            required: true,
        },
        rch: {
            type: Object,
            required: true,
        },
        rights: {
            type: Object,
            required: true,
        },
    },
    created: function() {
        console.log(this.rch.children)
    },
}
</script>

<style lang="scss" scoped>
.childBox {
    margin-left: 1rem;
}
.parent {
    font-weight: bold;
    font-size: 1.25rem;
}
li {
    text-align: left;
    margin: 0.5rem 0;
    display: flex;
    border: none;
    align-items: center;
    font-size: 1rem;
    display: flex;
    justify-content: flex-start;
    strong {
        padding: 0 0.5rem;
    }
    u {
        font-size: 0.85rem;
        margin: 0 0.5rem;
    }
}
</style>
