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
      <div class="festDetails">
        <div class="venue">{row.name}</div>
        <div class="activities">{row.activities}</div>
        {#await row.attendees then attendeesValue}
          <div class="attendees">
            {#each attendeesValue.rows as row}
              <p class="attendee">{row.name}</p>
            {/each}
          </div>
        {/await}
      </div>
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
    gap: 0.5rem;
    margin: 1.5rem auto 0 auto;
  }

  .festDetails {
    border-left: black solid 0.2rem;
    border-right: black solid 0.2rem;
    border-bottom: black solid 0.2rem;
    padding: 0.5rem 0.25rem;
  }

  .year{
    display: flex;
    align-items: center;
    background-color: #DE0000;
    border-left: black solid 0.2rem;
  }

  .title {
    display: flex;
    align-items: center;
    background-color: #DE0000;
    border-right: black solid 0.2rem;
  }

  h1{
    font-size: 2rem;
		font-family: carbonBlock;
    margin: 0;
    padding: 0.05rem 0.25rem;
  }

	h2 {
		font-size: 1.5rem;
		font-family: carbonBlock;
    text-transform: uppercase;
    margin: 0;
    text-align: center;
    padding: 0.05rem 0.25rem;
	}

  .venue {
    text-align: center;
    font-family: 'Jost', sans-serif;
    font-weight: bold;
  }

  .activities {
    text-align: center;
    font-family: 'Jost', sans-serif;
    font-style: italic;
  }

  .attendees {
    text-align: center;
  }

	p {
		font-family: 'Jost', sans-serif;
    display: inline;
	}

  .attendee + .attendee:before {
    content: ", ";
  }
</style>