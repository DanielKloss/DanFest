<script>
  import * as apiConfig from './apiConfig.json'

  async function getAttendees(year) {
    const attendeesResult = await fetch(apiConfig.attendeesByYear + year);
		return await attendeesResult.json();
  }

  async function getAllFests() {
    const festsResult = await fetch(apiConfig.allFests);
    let fests = await festsResult.json();
    for (let i = 0; i < fests.rows.length; i++) {
      fests.rows[i].attendees = getAttendees(fests.rows[i].year);
    }
    return fests;
  }

  let fests = getAllFests();
</script>

<main>
  {#await fests then festsValue}
    {#each festsValue.rows as row}
      <div class="festHeader">
        <div class="year">
          <h1>{row.year}</h1>
        </div>
        <div class="title">
          <h2>{row.title}</h2>
        </div>
      </div>
      <div class="venue">{row.name}</div>
      {#await row.attendees then attendeesValue}
        {#each attendeesValue.rows as row}
          <p class="attendee">{row.name}</p>
        {/each}
      {/await}
    {/each}
  {/await}
</main>

<style>
  main {
		width:70%;
		max-width: 500px;
		margin:0 auto;
	}
	
  .festHeader{
    display:flex;
    align-items: stretch;
    gap: 0.5em;
    margin: 0.5em auto;
  }

  .year{
    display: flex;
    align-items: center;
    background-color: #DE0000;
  }

  .title {
    display: flex;
    align-items: center;
    background-color: #DE0000;
  }

  h1{
    font-size: 4em;
		font-family: carbonBlock;
    margin: 0;
    padding: 0.05em 0.25em;
  }

	h2 {
		font-size: 2em;
		font-family: carbonBlock;
    text-transform: uppercase;
    margin: 0;
    text-align: center;
    padding: 0.05em 0.25em;
	}

  .venue {
    text-align: center;
    font-family: 'Jost', sans-serif;
    font-weight: bold;
  }

	p {
		font-family: 'Jost', sans-serif;
    display: inline;
	}

  .attendee + .attendee:before {
    content: ", ";
  }
</style>