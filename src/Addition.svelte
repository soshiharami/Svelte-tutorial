<div>
    <input type="text" bind:value={number1}>
    <input type="text" bind:value={number2}>
    <h4>
        {parseFloat(number1)} + {parseFloat(number2)} = {parseFloat(number1)+ parseFloat(number2)}
    </h4>
</div>

<script>
    let number2 = 0;
    let number1 = 0;
</script>
