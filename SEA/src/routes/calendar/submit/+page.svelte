

<script>
    import Calendar from '@event-calendar/core';
    import TimeGrid from '@event-calendar/time-grid';
    import Interaction from '@event-calendar/interaction';
    import '@event-calendar/core/index.css';
    export let cal;
    
    let plugins = [TimeGrid, Interaction];
    let options = {
        view: 'timeGridWeek',
        events: createEvents(),
        editable: false,
        selectable: false,
        slotMinTime: '08:00:00',
        slotMaxTime: '20:00:00',
        flexibleSlotTimeLimits:true,

    };

    function createEvents() {

        let days = [];
        for (let i = 0; i < 7; ++i) {
            let day = new Date();
            let diff = i - day.getDay();
            day.setDate(day.getDate() + diff);
            days[i] = day.getFullYear() + "-" + _pad(day.getMonth()+1) + "-" + _pad(day.getDate());
        }

        return [
            {start: days[1] + " 12:00", end: days[1] + " 14:00", resourceId: 2, backgroundColor: '#588157'},
            {start: days[2] + " 17:00", end: days[2] + " 24:00", resourceId: 1, backgroundColor: '#5A9F68'},
            {start: days[0] + " 10:00", end: days[0] + " 14:00", resourceId: 1, backgroundColor: '#BBD58E'},
            {start: days[1] + " 16:00", end: days[1] + " 18:00", resourceId: 2, backgroundColor: '#588157'},
            {start: days[2] + " 09:00", end: days[2] + " 13:00", resourceId: 2, backgroundColor: '#5A9F68'},
            {start: days[3] + " 14:00", end: days[3] + " 20:00", resourceId: 1, backgroundColor: '#3A5A40'},
            {start: days[5] + " 10:00", end: days[5] + " 16:00", resourceId: 2, backgroundColor: '#588157'},
            {start: days[5] + " 18:00", end: days[5] + " 21:00", resourceId: 2, backgroundColor: '#588157'},
        ];

    }

    function _pad(num) {
        let norm = Math.floor(Math.abs(num));
        return (norm < 10 ? '0' : '') + norm;
    }

</script>

<main class="row">
    <h1>Thank you for submitting. 4 people have submitted their availabilities so far and here are the best times to meet:</h1>
    <enhanced:img
        src="../../../lib/key.png?w=280"
    />
    <Calendar bind:this={cal} {plugins} {options} />
</main>
    


