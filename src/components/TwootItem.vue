<template>
    <div class="twoot-item" @click="favoriteTwoot(twoot.id)">
        <h3>@{{ username }}</h3>
        <p>{{ twoot.content }}</p>
    </div>
</template>

<script>
    
    export default {
        name: "TwootItem",
        props: {
            username: {
                type: String,
                required: true,
            },
            twoot: {
                type: String,
                required: true
            }
        },
        methods: {
            favoriteTwoot(id) {
                this.$emit('favorite', id)
            }
        }
    }
</script>

<style>
.twoot-item {
    background: white;
    padding: 10px 20px;
    width: 500px;
    margin-bottom: 20px;
    border-radius: 10px;
    transition: all 0.3s ease-in-out;
    cursor: pointer;
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif
}

.twoot-item:hover {
    width: 600px;
    transform: translateX(-50px);
}
</style>