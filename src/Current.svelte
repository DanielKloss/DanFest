<script>
	import * as apiConfig from './apiConfig.json'
	import * as animateScroll from "svelte-scrollto";

	async function getInvites() {
		const invitesResult = await fetch(apiConfig.invites2021);
		return await invitesResult.json();
	}

	let invites = getInvites();

	let invitationCode;
	let attending = "Attending";
	let shooting = "zombies";

	async function updateInvite() {
		let zombies = shooting=="zombies"?true:false;
		let updatedInvite = { 
			invitationCode:invitationCode.toLowerCase(),
			attending:attending,
			shooting:zombies
		}
		await fetch(apiConfig.updateInvite, {method: 'POST', body: JSON.stringify(updatedInvite), headers: {'Content-Type': 'application/json'}});
		invites = getInvites();
		invitationCode = ""
		attending = "Attending";
		shooting = "zombies";
		animateScroll.scrollTo({element: '.attendee'});
	}
</script>

<main>
	<h2>18th December 2021</h2>
	<p>In 2020 DanFest went virtual. In 2021 DanFest is taking one step back towards the real world. You have been selected to participate in a VR experience at <a href="https://www.navrtar.com/">Navrtar</a> in Ealing on 18th December. There is limited availability in the VR team but plus ones are welcome to the after party at a pub in Ealing.</p>
	<p>The experience and food will be included in your DanFest2021 ticket</p>
	<p>Please enter your invitation code, choose whether you want to shoot zombies or aliens and RSVP below</p>
		
	<div class="form">
		<input type="text" bind:value={invitationCode} placeholder="Enter your invitation code">
		<div class="formContainer attendingContainer" class:notAttending="{attending === 'Not Attending'}">
			<input type="radio" name="attendingStatus" id="attending" bind:group={attending} value={'Attending'} checked>
			<label for="attending">Attending</label>
			<input type="radio" name="attendingStatus" id="notAttending" bind:group={attending} value={'Not Attending'}>
			<label for="notAttending">Not Attending</label>
		</div>

		<div class="formContainer shootingContainer" class:aliens="{shooting === 'aliens'}">
			<input type="radio" name="shoot" id="zombies" bind:group={shooting} value={'zombies'} checked>
			<label for="zombies">Zombies</label>
			<input type="radio" name="shoot" id="aliens" bind:group={shooting} value={'aliens'}>
			<label for="aliens">Aliens</label>
		</div>

		<button on:click={updateInvite}>RSVP</button>
	</div>
	{#await invites then invitesValue}
    	{#each invitesValue.rows as row}
    		<div class="attendee" class:attendingStatus="{row.attending == 'Attending'}" class:notAttendingStatus="{row.attending == 'Not Attending'}">
				<p>{row.name}</p>
				<p>{row.attending}</p>	
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
	
	h2 {
		text-align:center;
		font-size: 2em;
		font-family: carbonBlock;
		background-color: #DE0000;
	}

	p {
		text-align:center;
		font-family: 'Jost', sans-serif;
	}
	
	.form {
		display: flex;
		flex-direction: column;
		gap: 1em;
		width: 75%;
		margin: 0 auto;
		padding: 10px;
		min-width: 185px;
	}
	
	button {
		background: red;
		transition: all 0.2s ease;
		padding: 10px;
		border: black 0.2em solid;
		font-family: carbonBlock;
		font-size: 1.5em;
	}
	
	input[type=text]{
		transition: all 0.2s ease;
		padding: 10px;
		font-family: 'Jost', sans-serif;
		text-align: center;
		font-weight: 900;
	}
	
	.attendee{
		display: flex;
		justify-content: space-between;
		padding-left: 1em;
		padding-right: 1em;
		margin: 1em auto;
		border: black 0.1em solid;
		background: linear-gradient(to right, red 50%, #EFB700 50%);
		width: 75%;
		transform: skewX(-10deg);
	}
	
	.formContainer {
		display: inline-flex;
		justify-content: space-between;
		transition: all 0.2s ease;
		padding: 10px;
		font-family: 'Jost', sans-serif;
	}
	
	.attendingContainer {
		background: #008450;
	}
	
	.shootingContainer{
		background: #869784;
	}
	
	.aliens {
		background: #B26DCC;
	}
	
	.attendingStatus {
		background: linear-gradient(to right, red 50%, #008450 50%);
	}
	
	.notAttendingStatus {
		background: linear-gradient(to right, red 50%, #B81D13 50%);
	}
	
	.notAttending {
		background: #B81D13;
	}
	
  	input[type=radio] {
    	display: none;
  	}

	label[for=aliens], label[for=zombies]{
    	cursor: pointer;
		color: rgba(0,0,0,0.2);
		transition: all 0.2s ease;
		font-size:0.9em;
	}

	input:checked + label[for=aliens] {
    	color: #fff;
  	}

  	input:checked + label[for=zombies] {
    	color: #fff;
  	}

	label[for=attending], label[for=notAttending]{
    	cursor: pointer;
		color: rgba(0,0,0,0.2);
		transition: all 0.2s ease;
		font-size:0.9em;
	}

	input:checked + label[for=attending] {
    	color: #fff;
  	}
  	
	input:checked + label[for=notAttending] {
    	color: #fff;
  	}
</style>