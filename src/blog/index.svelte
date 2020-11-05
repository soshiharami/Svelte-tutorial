<script>
    let BlogData
    const userAction = async () => {
        const response = await fetch('https://qiita.com/api/v2/users/soshi_harami/items');
        BlogData = await response.json(); //extract JSON from the http response
        console.log(BlogData)
        // do something with myJson
    }
</script>

{BlogData[0]}



