<script>
	
	export let elementStruct
	
	let cats = elementStruct.categories
	let traits = elementStruct.traits
	let effects = elementStruct.effects
</script>

<label for="name">Name:</label>
<input id="name" bind:value={elementStruct.name}>
<label for="quality">Quality:</label>
<input id="quality" type="number" min=1 max=999 bind:value={elementStruct.quality}/>
<hr/>
<label for="ec-el">Elemental:</label>
<input id="ec-el" type="number" bind:value={elementStruct.ec[0]}/>
<label for="ec-te">Terrestrial:</label>
<input id="ec-te" type="number" bind:value={elementStruct.ec[1]}/>
<label for="ec-ce">Celestial:</label>
<input id="ec-ce" type="number" bind:value={elementStruct.ec[2]}/>
<hr/>
{#each cats as cat,i}
<input bind:value={cats[i]}/><button on:click={()=>{cats.splice(i, 1); cats = cats}}>X</button><br/>
{/each}
<button on:click={()=>cats = [...cats, ""]}>Add category</button>
<hr/>
{#each traits as trait,i}
<input bind:value={traits[i]}/><button on:click={()=>{traits.splice(i, 1); traits = traits}}>X</button><br/>
{/each}
<button on:click={()=>traits = [...traits, ""]}>Add trait</button>
<hr/>
{#each effects as effect,i}
<input bind:value={effects[i]}/><button on:click={()=>{effects.splice(i, 1); effects = effects}}>X</button><br/>
{/each}
<button on:click={()=>effects = [...effects, ""]}>Add effect</button>