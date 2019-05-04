<template>
    <div class="calendar">
        <div class="tableHeader">
            <last-month-btn @toLastMonth="toLastMonth"></last-month-btn>
            <p class="displayMonth">{{ displayYear }}年{{ displayMonth }}月</p>
            <next-month-btn @toNextMonth="toNextMonth"></next-month-btn>
        </div>
        <table class="table calendarMain">
            <calendar-head></calendar-head>
            <calendar-body :displayDate="displayDate" :displayMonth="displayMonth"></calendar-body>
        </table>
    </div>
</template>

<script>
    import LastMonthBtn from './LastMonthBtn.vue'
    import NextMonthBtn from './NextMonthBtn.vue'
    import CalendarHead from './calendarHead/CalendarHead.vue'
    import CalendarBody from './calendarBody/CalendarBody.vue'

    export default {
        name: 'Calendar',
        components: {
            LastMonthBtn,
            NextMonthBtn,
            CalendarHead,
            CalendarBody,
        },
        data () {
            return {
                displayDate: new Date(),
                dummy: 1,
            }
        },
        methods: {
            toNextMonth: function () {
                const oldMonth = this.displayDate.getMonth();
                this.displayDate.setDate(1);
                this.displayDate.setMonth(oldMonth + 1);
                this.dummy++;
            },
            toLastMonth: function () {
                const oldMonth = this.displayDate.getMonth();
                this.displayDate.setDate(1);
                this.displayDate.setMonth(oldMonth - 1);
                this.dummy++;
            }
        },
        computed: {
            displayMonth: function () {
                const dummy = this.dummy;
                return this.displayDate.getMonth() + 1;
            },
            displayYear: function () {
                const dummy = this.dummy;
                return this.displayDate.getFullYear();
            }
        },
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .calendar {
        width: 80vw;
        margin-left: auto;
        margin-right: auto;
    }
    .tableHeader {
        display: flex;
        justify-content: space-between;
        margin-bottom: 2vh;
    }
    .calendarMain {
        box-shadow: 0 3px 5px rgba(0, 0, 0, 0.22);
    }
    .displayMonth {
        font-size: 4.5rem;
    }
</style>
