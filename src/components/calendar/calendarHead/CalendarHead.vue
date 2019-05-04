<template>
    <thead>
        <weekDay v-for="wDay,i in weekDays" v-bind:key="i" v-bind:wDay="wDay"></weekDay>
    </thead>
</template>

<script>
    import WeekDay from './WeekDay.vue'

    export default {
        data () {
            return {
                weekDays: ['日', '月', '火', '水', '木', '金', '土'],
            }
        },
        components: {
            WeekDay,
        }
    }
</script>
