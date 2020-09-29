<template>
    <li :style="{ margin: '0 0 1rem' + ' ' + rule.parentID + 'rem' }" appear>
        <input
            type="checkbox"
            :indeterminate="rule.indeterminate"
            :checked="rule.checked"
            v-on:change="$emit('change-parent', rule)"
            :id="rule.id"
        />
        <label
            :for="rule.id"
            v-bind:title="
                'id этого элемента: ' +
                    rule.id +
                    ' | id родителя: ' +
                    rule.parentID
            "
        >
            {{ rule.name }}
        </label>
    </li>
</template>

<script>
export default {
    // name: 'recursive-rule',
    methods: {},
    props: {
        rule: {
            type: Object,
            required: true,
        },
        rights: {
            type: Object,
            required: true,
        },
        showInfo: {
            type: Boolean,
            required: true,
        },
    },
}
</script>

<style lang="scss" scoped>
.parent {
    font-weight: bold;
    font-size: 1.25rem;
}
li {
    text-align: left;
    border: none;
    font-size: 1.1rem;
    display: flex;
    justify-content: flex-start;
    align-items: center;
    strong {
        padding: 0 0.5rem;
    }
    u {
        font-size: 0.66rem;
        margin: 0 0.5rem;
        text-decoration: none;
    }
    input[type='checkbox'] {
        margin: 0 1rem;
        width: 1.25rem;
        height: 1.25rem;
        background-color: yellow;
        cursor: pointer;
    }
    label {
        cursor: pointer;
    }
}
</style>
