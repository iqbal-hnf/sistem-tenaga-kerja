<script>
	export let id = '';
	export let classList = '';
	
    export let type= "button"
    export let custom = ""
    export let disabled=""
    export let onClick = () => {}
    const handleClick = (evt) => {
		onClick(evt);
	};

</script>
<button type={type} id={id} class={classList} on:click={handleClick} {disabled} style={custom}>

	<slot />
</button>

<style>
button {
    border : 1px solid transparent;
    border-radius: 8px;
    cursor: pointer;
    font-size: 16px;
    padding: 8px 24px;
    background-color: transparent;
   
}

.btn-primary{
    background-color: #2d3e50;
    color: #fff;
}
.btn-secondary{
    background-color: 1px solid white;
    color: #2d3e50;
}
.btn-card-header{
    background-color: transparent;
    border: 1px solid #fff;
    color: #fff;
    border-radius: 5px;
    font: bold;
}
.btn-section{
    background-color: transparent;
    border-radius: 10px;
    color: black;
    border: 2px solid #00195E;
    height: 42px;
    width: fit-content;
    margin-top: 35px;
    font-weight: 300;
    font-size: 16px;
}

.btn-secondary:hover{
    background-color: #2d3e50;
    color: #fff;
}


	
</style>