<template>
    <div class="picture-container">
        <img class="hidden-picture" v-if="itemID" :src="src" alt="picture">
        <img class="fade-in" v-if="itemID && showPicture" :src="src" alt="picture">
    </div>

</template>

<script>
    export default {
        props: {
            itemID: Number,
            showPicture: Boolean
        },
        data() {
            return {

            }
        },
        computed: {
            src() {
                return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.itemID}.svg`
            }
        }
    }
</script>