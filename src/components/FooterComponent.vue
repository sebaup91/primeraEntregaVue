<template>
    <footer>
        <p> {{ mensaje }}</p>
    </footer>
</template>
<script>
export default {
    name: "FooterComponent",
    props: {
        mensaje: String
    }
}
</script>
<style scoped>
    footer {
        background-color: aquamarine;
    }
</style>