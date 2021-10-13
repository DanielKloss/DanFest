<script>
  async function getLocations() {
    const locationsResult = await fetch('http://192.168.1.123:3000/danfest/apilocations');
		return await locationsResult.json();
  }

  async function getAttendees(year) {
    const attendeesResult = await fetch('http://192.168.1.123:3000/danfest/apiattendees?year=' + year);
		return await attendeesResult.json();
  }

  let locations = getLocations();
  let attendees2020 = getAttendees("2020");
</script>

<main>
  {#await locations then value}
    {#each value.rows as row}
      <p>{row.name}</p>
    {/each}
  {/await}
  {#await attendees2020 then value}
    {#each value.rows as row}
      <p>{row.name}</p>
    {/each}
  {/await}
    <!-- <ul>
        {#each history as event}
          <h2>{event.year} - {event.title}</h2>
            <ul>
                {#each event.venues as venue}
                  <p class="venue">{venue}</p>
                {/each}
            </ul>
            <p class="description">{event.description}</p>
            <ul>
              {#each event.attendees as attendee}
                <p class="attendee">{attendee}</p>
              {/each}
            </ul>
        {/each}
    </ul> -->
</main>

<style>
  main {
		width:70%;
		max-width: 500px;
		margin:0 auto;
	}
	
	h2 {
		text-align:center;
		font-size: 2em;
		font-family: carbonBlock;
		background-color: #DE0000;
    text-transform: uppercase;
    margin-bottom: 0.25em;
	}

  ul {
    padding-left: 0;
    text-align: center;
  }

	p {
		font-family: 'Jost', sans-serif;
    display: inline;
	}

  .venue {
    font-weight: bold;
    font-size: 1.25em;
  }

  .description{
    font-style: italic;
  }

  .venue ~ .venue:before {
    content: ", ";
  }

  .attendee ~ .attendee:before {
    content: ", ";
  }
</style>