<template>
    <div>
        <h2>{{ title }}</h2>
        <p>{{ description }}</p>
        <p>Directed by: {{ director }}</p>
        <p>Avg rating: {{ rating }}</p>
    </div>
</template>

<script>
export default {

    props: {
        title: String,
        rating: Number,
        description: String,
        director: String
    }
}
</script>

<style>

</style>


