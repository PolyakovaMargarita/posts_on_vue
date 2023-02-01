<template>
    <select v-model="modelValue" @change="changeOptions">
        <option disabled value="">Select</option>
        <option 
            v-for="option in options"
            :key="option.value"
            :value="option.value"
        >{{ option.name }}</option>
    </select>
</template>

<script>
export default {
    name: "my-select",
    modal: {
        modelValue: {
            type: String
        },
        option: {
            type: Array,
            default: () => []
        }
    },
    methods: {
        changeOptions(event) {
            this.$emit('update:modelValue', event)
        }
    }
}

</script>

<style>
/* .selest {
    width: 100px;
    padding: 10px 15px;
    background: none;
    border: 1px solid teal;
    color: teal;
    text-align: center;
} */
</style>