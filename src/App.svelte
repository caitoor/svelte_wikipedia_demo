<script>
  let animalName = "";
  let excerpt = "";

  async function fetchExcerpt(animal) {
    const response = await fetch(
      `https://en.wikipedia.org/api/rest_v1/page/summary/${animal}`,
    );
    const data = await response.json();
    return data.extract;
  }
</script>

<input type="text" bind:value={animalName} placeholder="Enter animal name" />
<button
  on:click={async () => {
    excerpt = await fetchExcerpt(animalName);
  }}>Submit</button
>

<p>{excerpt}</p>
