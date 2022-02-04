<script>
	import { createEventDispatcher } from 'svelte';
    export let title, price, bestseller = false
    const dispatch = createEventDispatcher();

    function addToCart(){
        // dispatch event name and optional data
        dispatch('add-to-cart', {id: 'p1'} )
    }
    function deleteItem(){
        dispatch('delete-item', {id: 'p1'})
    }
</script>
<article>
    <h1>{title}</h1>
    <h2>${price}</h2>
    {#if bestseller}
        <h3>BestSeller</h3>
    {/if}
    <button on:click={addToCart}>Add to Cart</button>
    <button on:click={deleteItem}>Delete Product</button>
</article>