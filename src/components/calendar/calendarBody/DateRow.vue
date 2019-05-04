<template>
    <tr>
        <td class="calendarCell calendarTd" v-for="date,i in rowData" v-bind:key="i" :class="{today:isToday(date)}">{{ date }}</td>
    </tr>
</template>

<script>
    export default {
        data () {
            return {
                today: new Date(),
            }
        },
        props: {
            index: Number,
            displayDate: Date,
            displayMonth: Number
        },
        methods: {
            isToday: function (date) {
                const thisMonth = this.today.getMonth() + 1,
                    displayYear = this.displayDate.getFullYear(),
                    displayMonth = this.displayMonth,
                    today = this.today;

                if (thisMonth === displayMonth && today.getFullYear() === displayYear && today.getDate() === date) {
                    return true;
                }
            }
        },
        computed: {
            monthDays: function () {
                const dummy = this.dummy;
                const month31 = [1, 3, 5, 7, 8, 10, 12];
                const month30 = [4, 6, 9, 11];
                const displayDate = this.displayDate;
                const displayMonth = this.displayMonth;

                const startWeekDay = function () {
                    displayDate.setDate(1);
                    return displayDate.getDay();
                };
                const fillInBlank = function (array) {
                    for (let i = 0; i < startWeekDay(); i++) {
                        array.push(0);
                    };
                    return array;
                };
                const makeMonthDaysOf = function (num) {
                    let array = [];
                    array = fillInBlank(array);
                    for (let i = 1; i < num + 1; i++) {
                        array.push(i);
                    };
                    return array;
                };

                if (month31.includes(displayMonth)) { return makeMonthDaysOf(31); }
                if (month30.includes(displayMonth)) { return makeMonthDaysOf(30); }
                if (displayMonth === 2) {
                    if (this.displayDate.getFullYear() % 4 === 0) {
                        return makeMonthDaysOf(29);
                    }
                    return makeMonthDaysOf(28);
                }
            },
            rowData: function () {
                const dummy = this.dummy;
                const monthDays = this.monthDays,
                    rowNum = this.index;
                let rowData = [];;

                switch (rowNum) {
                    case 1:
                        var loopStartNum = 0,
                            loopEndNum = 7;
                        break;
                    case 2:
                        var loopStartNum = 7,
                            loopEndNum = 14;
                        break;
                    case 3:
                        var loopStartNum = 14,
                            loopEndNum = 21;
                        break;
                    case 4:
                        var loopStartNum = 21,
                            loopEndNum = 28;
                        break;
                    case 5:
                        var loopStartNum = 28,
                            loopEndNum = 35;
                        break;
                    case 6:
                        var loopStartNum = 35,
                            loopEndNum = 42;
                        break;
                }
                for (let i = loopStartNum; i < loopEndNum; i++) {
                    let data = monthDays[i];
                    if (data === 0) {
                        rowData.push(null);
                    } else {
                        rowData.push(data);
                    }
                }
                return rowData;
            },
        },
    }
</script>

<style scoped>
    .calendarTd {
        padding: 0 8px 8vh !important;
    }
    .calendarCell {
        text-align: center;
        /* border: 3px solid; */
    }
    .today {
        background-color: #14d7ed;
    }
</style>