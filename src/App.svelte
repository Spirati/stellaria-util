<script>
	import Element from "./Element.svelte"
	
	class ElementClass {
		constructor() {
			this.name = "New Element"
			this.ec = [0, 0, 0]
			this.traits = []
			this.effects = []
			this.categories = []
			this.quality = 0
		}
		serialize() {
			return {
				name: this.name,
				quality: this.quality,
				ec: this.ec,
				traits: this.traits,
				categories: this.categories
			}
		}
	}
	class InventoryItem {
		constructor() {
			this.itemID = 0
			this.quantity = 1
		}
		serialize() {
			return {
				id: this.itemID,
				quantity: this.quantity
			}
		}
	}
	
	let elements = [new ElementClass()]
	let inventory = [new InventoryItem()]
	let serialized = ["",""]
</script>

<div class="row">
	<div class="column">
		<h1>Elements</h1>
		{#each elements as el,i}
		<h3>
			Element {i+1} <button on:click={()=>{elements.splice(i, 1); elements = elements}}>X</button>
		</h3>
		<Element elementStruct={el}/>
		{/each}
		<br/><br/>
		<button on:click={()=>elements = [...elements, new ElementClass()]}>New element</button>
		<br/>
	</div>
	<div class="column">
		<h1>Inventory</h1>
		{#each inventory as item, i}
		<label for="inventory-{i}">Item:</label>
		<select id="inventory-{i}" bind:value={item.itemID}>
			{#each elements as el, j}
				{#if j == item.itemID}
				<option value="{j}" selected>{el.name}</option>
				{:else}
				<option value="{j}">{el.name}</option>
				{/if}
			{/each}
		</select>
		<label for="quantity-{i}">Quantity:</label>
		<input type="number" id="quantity-{i}" min=1 bind:value={item.quantity}>
		<button on:click={()=>{inventory.splice(i, 1); inventory = inventory}}>X</button>
		{/each}
		<br/><br/>
		<button on:click={()=>inventory = [...inventory, new InventoryItem()]}>Add item</button>
	</div>
</div>


<button on:click={
	()=>{
		serialized = [JSON.stringify(elements.map(e=>e.serialize())), JSON.stringify(inventory.map(e=>e.serialize()))]
	}
}>Serialize</button>
<hr/>
<code>
{serialized[0]}<br/>{serialized[1]}
</code>

<style>
	.row {
		display: flex;
		flex-direction: row;
		flex: 1;
	}
	.column {
		flex: 50%;
		border: 1px black solid;
		overflow: auto;
		height: 80vh;
	}
</style>
