


<script>
    import Calendar from '@event-calendar/core';
    import TimeGrid from '@event-calendar/time-grid';
    import Interaction from '@event-calendar/interaction';
    import '@event-calendar/core/index.css';
    import Button from '@smui/button';
    import { browser } from '$app/environment';
    import { goto } from '$app/navigation';
    export let cal;
    let plugins = [TimeGrid, Interaction];
    let options = {
        view: 'timeGridWeek',
        events: [],
        //pointer: true,
        eventStartEditable: true,
        editable: true,
        selectable: true,

        select: function (info) {cal.addEvent(info)}, // cal.add event to confirm an event to add
        eventClick: function (info) { removeEvent(info)}

    };

    function removeEvent(){
        cal.removeEventById(info.event.id)
    }

    function _pad(num) {
        let norm = Math.floor(Math.abs(num));
        return (norm < 10 ? '0' : '') + norm;
    }

    const CLIENT_ID = '591983148481-03ba760usd8mv1534pr6b83l4l94hjup.apps.googleusercontent.com';
    const API_KEY = 'AIzaSyB_l63gYXH3mQw8G3PIDpy9AZbg7rJziWY';

    // Discovery doc URL for APIs used by the quickstart
    const DISCOVERY_DOC = 'https://www.googleapis.com/discovery/v1/apis/calendar/v3/rest';

    // Authorization scopes required by the API; multiple scopes can be
    // included, separated by spaces.
    const SCOPES = 'https://www.googleapis.com/auth/calendar.readonly';

    let tokenClient;
    let gapiInited = false;
    let gisInited = false;

    /**
     * Callback after api.js is loaded.
     */
    function gapiLoaded() {
        gapi.load('client', initializeGapiClient);
    }

    /**
     * Callback after the API client is loaded. Loads the
     * discovery doc to initialize the API.
     */
    async function initializeGapiClient() {
    await gapi.client.init({
        apiKey: API_KEY,
        discoveryDocs: [DISCOVERY_DOC],
    });
    gapiInited = true;
    maybeEnableButtons();
    }

    /**
     * Callback after Google Identity Services are loaded.
     */
    function gisLoaded() {
    tokenClient = google.accounts.oauth2.initTokenClient({
        client_id: CLIENT_ID,
        scope: SCOPES,
        callback: '', // defined later
    });
    gisInited = true;
    maybeEnableButtons();
    }

    /**
     * Enables user interaction after all libraries are loaded.
     */
    function maybeEnableButtons() {
    if (gapiInited && gisInited) {
        document.getElementById('authorize_button').style.visibility = 'visible';
    }
    }

    /**
     *  Sign in the user upon button click.
     */
    function handleAuthClick() {
        tokenClient.callback = async (resp) => {
            if (resp.error !== undefined) {
            throw (resp);
            }
            //document.getElementById('signout_button').style.visibility = 'visible';
            //document.getElementById('authorize_button').innerText = 'Sync another calendar';
            
            //await listUpcomingEvents();
        };

        if (gapi.client.getToken() === null) {
            // Prompt the user to select a Google Account and ask for consent to share their data
            // when establishing a new session.
            tokenClient.requestAccessToken({prompt: 'consent'});
        } else {
            // Skip display of account chooser and consent dialog for an existing session.
            tokenClient.requestAccessToken({prompt: ''});
        }
        goto('/calendar/synced')
    

}

    /**
     *  Sign out the user upon button click.
     */
    function handleSignoutClick() {
    const token = gapi.client.getToken();
    if (token !== null) {
        google.accounts.oauth2.revoke(token.access_token);
        gapi.client.setToken('');
        document.getElementById('content').innerText = '';
        document.getElementById('authorize_button').innerText = 'Authorize';
        document.getElementById('signout_button').style.visibility = 'hidden';
    }
    }
  
    const initializeGapi = async () => {
      gapi.load('client', start);
    }
  </script>
  
  <svelte:head>
    <script src="https://apis.google.com/js/api.js" on:load={gapiLoaded}></script>
    <script src="https://accounts.google.com/gsi/client" on:load={gisLoaded}></script>
  </svelte:head>

  

  <header class="row">
    
        <Button on:click={handleAuthClick}>
            Sync Google Calendar
        </Button>


    </header>
    <main class="row">
        <Calendar bind:this={cal} {plugins} {options} />
    </main>
    

