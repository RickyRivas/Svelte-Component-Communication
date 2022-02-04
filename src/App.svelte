<script>
	import Modal from './Modal.svelte';
	import Product from './Product.svelte';
	let showModal = false;
	let closeable = false;
	let products = [
		{
			id: 'p1',
			title: 'A Book',
			price: 12.99
		}
	]
	function addToCart(e){
		console.log(e)
	}
	function deleteProduct(e){
		console.log(e)
	}
</script>

{#each products as product}
	<Product 
	title={product.title}
	price={product.price} 
	on:add-to-cart={addToCart}
	on:delete-item='{deleteProduct}'
	/>
{/each}

<button on:click={() => showModal = true}>Show Modal</button>


{#if showModal}
	<Modal 
		on:cancel='{() => showModal = false}' 
		on:close='{() => showModal = false}'
		let:didAgree={closeable}
		>
			<h1 slot='header'>Message:</h1>
			<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. A ex vitae ipsam, omnis voluptatem deleniti? Vero voluptas illum aspernatur explicabo!</p>
			<button slot='footer' on:click='{() => showModal = false}' disabled={!closeable}>Confirm</button>
	</Modal>
{/if}


