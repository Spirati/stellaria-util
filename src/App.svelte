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
	
	let elements = [new ElementClass()]
	let serialized = ""
</script>

{#each elements as el,i}
<h3>
	Element {i+1} <button on:click={()=>{elements.splice(i, 1); elements = elements}}>X</button>
</h3>
<Element elementStruct={el}/>
{/each}
<br/><br/>
<button on:click={()=>elements = [...elements, new ElementClass()]}>New element</button>
<br/>
<button on:click={()=>serialized = JSON.stringify(elements.map(e=>e.serialize()))}>Serialize</button>
<hr/>
<code>
{serialized}
</code>
