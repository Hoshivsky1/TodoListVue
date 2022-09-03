<template>
    <select v-model="modelValue" @change="changeOption">
        <option disabled value="">Виберіть зі списку</option>
        <option 
            v-for="option in options" 
            :key="option.value" 
            :value="option.value"
        >
            {{option.name}}
        </option>
    </select>
</template>
 
<script>
export default {
    name: 'my-select',
    props: {
        modelValue: {
            type: String
        },
        options: {
            type: Array,
            default: () => []
        }
    },
    methods: {
        changeOption (event) {
            this.$emit('update:modelValue', event.target.value)
        }
    }
}
</script>
 
<style scoped>
    select {
        border: 2px solid rgb(21, 174, 21);
        border-radius: 2px;
        height: 30px;
    }
</style>