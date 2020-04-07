<script>
    import Button from './Button.svelte';
    import { createEventDispatcher } from 'svelte';
    export   let productTitle;
    export   let productDesc;
    export   let productPrice;

    const dispatch = createEventDispatcher();
    
    function addToCart()
    {
        dispatch('addCart', productTitle);
    }

</script>

<style>
  
  div{
        margin: 1rem;
        box-shadow: 0 2px 8px rgba(0,0,0,0.26);
        padding: 1rem;
        border-radius: 5px;
        background: white;
    }

    h1{
        font-size: 1.25rem;
        margin: 0.25rem 0;
    }

    h2{
        font-size: 1rem;
        margin: 0.25rem 0;
        color: grey
    }

    p {
        margin: 0.25rem 0;
    }
</style>

<div>
    <h1>{productTitle}</h1>
    <h2>{productPrice}</h2>
    <p>{productDesc}</p>
    <button on:click{addToCart}>Add to Cart</button>
</div>