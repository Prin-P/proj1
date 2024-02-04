

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@event-calendar/build@2.6.1/event-calendar.min.css">

<script src="https://cdn.jsdelivr.net/npm/@event-calendar/build@2.6.1/event-calendar.min.js">
    import Calendar from '@event-calendar/core';
    import TimeGrid from '@event-calendar/time-grid';
    import Interaction from '@event-calendar/interaction';
    import '@event-calendar/core/index.css';

    let cal;
    let plugins = [TimeGrid, Interaction];
    let options = {
        view: 'timeGridWeek',
        events: [],
        pointer: true,
        eventStartEditable: true,
        editable: true,
        selectable: true,

        //select: function (info) {cal.addEvent(info)}, // cal.add event to confirm an event to add
        //dateClick: function (info) {cal.addEvent(info);},
       //eventDragStart: function (info) {console.log('dragStart');},
        //eventDragStop: function (info) {console.log('dragStop');},
        //eventDrop: function (info) {console.log('drop');},
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
            {start: days[0] + " 00:00", end: days[0] + " 09:00", resourceId: 1, display: "background"},
            {start: days[1] + " 12:00", end: days[1] + " 14:00", resourceId: 2, display: "background"},
            {start: days[2] + " 17:00", end: days[2] + " 24:00", resourceId: 1, display: "background"},
            {start: days[0] + " 10:00", end: days[0] + " 14:00", resourceId: 1, title: "The calendar can display background and regular events", color: "#FE6B64"},
            {start: days[1] + " 16:00", end: days[2] + " 08:00", resourceId: 2, title: "An event may span to another day", color: "#B29DD9"},
            {start: days[2] + " 09:00", end: days[2] + " 13:00", resourceId: 2, title: "Events can be assigned to resources and the calendar has the resources view built-in", color: "#779ECB"},
            {start: days[3] + " 14:00", end: days[3] + " 20:00", resourceId: 1, title: "", color: "#FE6B64"},
            {start: days[3] + " 15:00", end: days[3] + " 18:00", resourceId: 1, title: "Overlapping events are positioned properly", color: "#779ECB"},
            {start: days[5] + " 10:00", end: days[5] + " 16:00", resourceId: 2, title: "You have complete control over the <i><b>display</b></i> of events…", color: "#779ECB"},
            {start: days[5] + " 14:00", end: days[5] + " 19:00", resourceId: 2, title: "…and you can drag and drop the events!", color: "#FE6B64"},
            {start: days[5] + " 18:00", end: days[5] + " 21:00", resourceId: 2, title: "", color: "#B29DD9"},
            {start: days[1], end: days[3], resourceId: 1, title: "All-day events can be displayed at the top", color: "#B29DD9", allDay: true}
        ];
    }

    function createEvent(info) {
        curEvents = getEvents()
        
        plainOb = {start: info.start}
        eventOb = addEvent( plainOb )
        curEvents.append(eventOb)

        options.events.append(plainOb);

    }

    function _pad(num) {
        let norm = Math.floor(Math.abs(num));
        return (norm < 10 ? '0' : '') + norm;
    }

    // Add new events to calendar
    function updateOptions(info) {

        options.events.append({start: info.start, end: info.end});
    }

    function removeOptions(duration) {
        options.slotDuration = duration;
    }
</script>

<Calendar bind:this={cal} {plugins} {options} />