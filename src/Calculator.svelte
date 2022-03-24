<script>
	import Keypad from './Keypad.svelte';

	let pin;
	$: view = pin ?pin:'0'

	function handleSubmit() {
    //    alert( view.test(/^(.*[+,/,*,-])?$/igm));
   const lastChar=view[view.length-1]
       if(lastChar==='+'||lastChar==='-'||lastChar==='/'||lastChar==='*')
       {
           alert("Invalid operation");
           return;
       }
        console.log(view);
        console.log(eval(pin))
        
        view=eval(view);
		pin=eval(view);
        // alert(`submitted ${pin}`);
	}
</script>

<div>
<h1 style="color: {pin ? '#333' : '#ccc'}">{view}</h1>

<Keypad bind:value={pin} on:submit={handleSubmit}/>
</div>

<style>
h1{
height: 40px;
border: 1px solid grey;
width: 336px;
margin: 0px auto;
margin-bottom: 10px;
display: flex;
justify-content: flex-end;
padding: 5px;
border-radius: 5px;
}
</style>