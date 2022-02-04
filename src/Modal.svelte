<script>
	import { createEventDispatcher, onMount, onDestroy, beforeUpdate, afterUpdate } from 'svelte';
    const dispatch = createEventDispatcher();
    let agreed = false
    let autoscroll = false;
    onMount(() => {
        console.log('on mount')
    })
    onDestroy(() => {
        console.log('on destroy')
    })
    beforeUpdate(() => {
        autoscroll = agreed;
        console.log('before update')
    })
    afterUpdate(() => {
        console.log('after update')
        if(autoscroll){
            const modal = document.querySelector('.modal');
            modal.scrollTo(0, modal.scrollHeight)
        }
    })
</script>

<div class="backdrop" on:click={() => dispatch('cancel')}></div>
<div class='modal'>
    <header>
        <slot name='header'><!-- optional fallback --></slot>
    </header>
    <div class="content">
        <slot><!-- optional fallback --></slot>
    </div>
    <div class='disclaimer'>
        <p>Before you close, you need to agree to our temrs</p>
        <button on:click={() => agreed = true}>Agree</button>
    </div>
    <footer>
        <slot name='footer' didAgree={agreed}>
            <button on:click={() => dispatch('close')} disabled='{!agreed}'>Close</button>
        </slot>
    </footer>
</div>

<style>
    .backdrop {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background: rgba(0, 0, 0, 0.75);
  z-index: 10;
}
header {
    border-bottom: 1px solid #a4a4a4;
}
.modal {
  padding: 1rem;
  position: fixed;
  top: 10vh;
  left: 10%;
  width: 80%;
  max-height: 15vh;
  background: white;
  border-radius: 5px;
  z-index: 100;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  overflow: scroll;
}

</style>