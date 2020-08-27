<template>
    <b-navbar toggleable="lg" variant="light">
    <b-navbar-brand href="#">Todos App</b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
        <b-collapse id="nav-collapse" is-nav>

            <b-navbar-nav>
                <!-- <b-nav-item href="#">Link</b-nav-item> -->
                <!-- <b-nav-item href="#" disabled>Disabled</b-nav-item> -->
            </b-navbar-nav>

            <!-- Right aligned nav items -->
            <b-navbar-nav class="ml-auto">
                <input 
                    v-model="searchKey"
                    placeholder="Search..." 
                    class="form-control col-xs-10"
                    @keyup="$emit('search-item', $event.target.value)" />
                <button type="button"
                    class="btn btn-outline-secondary ml-2 col-xs-1"
                    @click="resetSearch">x</button>
            </b-navbar-nav>

        </b-collapse>
    </b-navbar>
</template>

<script>
    export default {
        name: 'Header',
        data() {
            return {
                searchKey: ''
            }
        },
        methods: {
            resetSearch() {
                this.searchKey='';
                this.$emit('reset-search');
            }
        }
    }
</script>