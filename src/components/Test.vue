<template>
    <div class="container">
        <ul>
            <li v-bind:key="item" v-for="item in mainText">{{item}}</li>
        </ul>
    </div>
</template>

<script>
export default {
    name: "Test",
    data() {
        return {
            mainText: ['apples', 'oranges', 'mangoes']
        };
    }
}
</script>