<template>
    <div>
        <input 
            v-model="searchTerm"
            v-on:keyup.enter="handleSearchEnter"
            placeholder="Search for software..." 
            type="text"
        />
        <ul>
            <li v-for="s in filteredSoftware" :key="s.id">
                {{ s.name }}
                <button v-on:click="s.selected = true">Add</button>
            </li>
        </ul>
        <ul>
            <li v-for="s in selectedSoftware" :key="s.id">
                {{ s.name }}
                <button v-on:click="s.selected = false">Remove</button>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    data() {
        return {
            // The search term being used to filter the list.
            searchTerm: '',

            // A master list of available software.
            software: [
                {
                    id: '1',
                    name: 'AVG',
                    selected: false,
                },
                {
                    id: '2',
                    name: 'AdobeCC',
                    selected: false,
                },
                {
                    id: '3',
                    name: '7-Zip',
                    selected: false,
                }
            ],
        };
    },
    methods: {
        handleSearchEnter() {
            // If the list has a top result, add it.
            if (this.filteredSoftware.length > 0) {
                this.filteredSoftware[0].selected = true;

                // Reset the search.
                this.searchTerm = '';
            }
        },
    },
    computed: {
        filteredSoftware: function() {
            // Filter software
            return this.software.filter(function(s) {
                return s.name.toLowerCase().includes(this.searchTerm.toLowerCase()) && !s.selected;
            }.bind(this));
        },
        selectedSoftware: function() {
            // Return the software that has been selected.
            return this.software.filter(function(s) {
                return s.selected;
            }.bind(this));
        }
    }
};
</script>