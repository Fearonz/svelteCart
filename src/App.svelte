<script>
	import Product from "./Product.svelte";
	import Button from './Button.svelte';
	import Cart from './Cart.svelte';

	let title = '';
	let price;
	let desc = '';

	let products = [];
	let cartItems = [];

	function setTitle(event)
	{
		title = event.target.value;
	}

	function createProduct()
	{
		const newProduct = {
			title: title,
			price: price,
			desc: desc
		};
		products = products.concat(newProduct);
	}

	function addToCart(event){
		const selectedTitle = event.detail;
		cartItems = cartItems.concat(
			{...products.find(prod => products.title === selectedTitle)
			});
			console.log(cartItems);
	}

</script>

<main>
	<section>
		<Cart items={cartItems}/>

	</section>

	<hr>

	<section>
			<div>
				<label for="title">Title</label>
				<input type="text" id="title" value="{title}" on:input="{setTitle}"/>
			</div>

			<div>
				<label for="price">Price</label>
				<input type="numbers" id="price" bind:value={price}/>
			</div>

			<div>
				<label for="description">Description</label>
				<textarea rows="3" id="desc" bind:value={desc}></textarea>
			</div>
		<button on:click={createProduct}>Create Product</button>
	</section>

	<section>
		{#if products.length === 0}
			<p>No Products are added yet!</p>
			{:else}
				{#each products as product}
					<Product 
					productTitle={product.title} 
					productDesc={product.desc} 
					productPrice={product.price}
					on:addcart={addToCart}/>
			{/each}
	{/if}
	</section>


</main>

<style>
	  button {
        font: inherit;
        padding: 0.15rem 0.5rem;
        background: magenta;
        border: 1px solid #d10057;
        color: white;
        cursor: pointer;
    }

    button:hover, button:active{
        box-shadow: 1px 1px 6px rgba(0,0,0,0.26);
    }

	section {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	label, input {
		width: 100%;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>

