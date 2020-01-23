<script context="module">
  export function preload(page) {
    return { year: page.params.year, id: page.params.id };
  }
</script>

<script>
  export let year;
  export let id;
</script>

<div>{year} {id}</div>
