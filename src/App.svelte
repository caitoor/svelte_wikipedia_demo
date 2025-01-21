<script>
  let animalName = "";
  let excerpt = "";
  let imageUrl = "";

  async function fetchExcerpt(animal) {
    const response = await fetch(
      `https://en.wikipedia.org/api/rest_v1/page/summary/${animal}`,
    );
    const data = await response.json();
    return { extract: data.extract, image: data.thumbnail ? data.thumbnail.source : '' };
  }
</script>

<input type="text" bind:value={animalName} placeholder="Enter animal name" />
<button
  on:click={async () => {
    const result = await fetchExcerpt(animalName);
    excerpt = result.extract;
    imageUrl = result.image;
  }}>Submit</button
>

<p>{excerpt}</p>
{#if imageUrl}
  <img src={imageUrl} alt={animalName} />
{/if}
