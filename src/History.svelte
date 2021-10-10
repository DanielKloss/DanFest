<script>
    let history = [
		{
			year:"2020",
      title: "The one that was Virtual",
      venues: ["Virtual"],
      description: "Pub Dinner and Quiz by Nom and Flight Club",
      attendees: ["Dan", "Georgie", "Mark", "Nom"]
    },
		{
    	year: "2019",
      title: "The one with the Inner Sanctum",
      venues: ["Friern Park"],
      attendees: ["Dan", "Georgie", "Nat", "Thomas", "Tash", "Tom"]
    },
		{
    	year: "2018",
      title: "The one where they threw Darts",
      venues: ["Pub", "Flight Club"],
      attendees: ["Dan", "Georgie", "Mark", "Nom"]
    },
		{
    	year: "2017",
      title: "The one where Nom fell asleep",
      venues: ["Friern Park"],
      attendees: ["Dan", "Georgie", "Mark", "Nom"]
    }
	];
</script>

<main>
    <ul>
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
    </ul>
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