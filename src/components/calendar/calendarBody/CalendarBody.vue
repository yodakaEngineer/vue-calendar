<template>
    <tbody>
        <dateRow v-for="i in 6" v-bind:key="i" v-bind:index="i" :displayDate="displayDate" :displayMonth="displayMonth"></dateRow>
    </tbody>
</template>

<script>
    import DateRow from './DateRow.vue'

    export default {
        props: {
            displayDate: Date,
            displayMonth: Number
        },
        components: {
            DateRow,
        }
    }
</script>