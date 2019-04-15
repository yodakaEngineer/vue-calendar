<template>
    <th class="calendarCell calendarTh">{{ wDay }}</th>
</template>

<script>
    export default {
        name: 'week-day',
        props: ['wDay'],
    }
</script>
