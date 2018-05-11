<template>
    <div>
        <input 
            v-model="searchTerm"
            v-on:keyup="handleSearch"
            v-on:keyup.enter="handleSearchEnter"
            placeholder="Search for software..." 
            type="text"
        />
        <button v-on:click="handleSearchEnter">Add</button>
        <div v-if="err">{{ errMsg }}</div>

        <h3>Available</h3>
        <ul>
            <li v-for="s in filteredSoftware" :key="s.id">
                {{ s.name }}
                <button v-on:click="s.selected = true">Add</button>
            </li>
        </ul>
        
        <h3>Selected</h3>
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

            // Data for handling error messages.
            err: false,
            errMsg: '',
        };
    },
    methods: {
        handleSearch(e) {
            // If enter wasn't pressed, reset the error message.
            if (e.keyCode !== 13) {
                this.resetError();
            }
        },
        handleSearchEnter() {
            // If the list has a top result, add it.
            if (this.filteredSoftware.length > 0) {
                this.filteredSoftware[0].selected = true;

                // Reset the search.
                this.searchTerm = '';
            } else {
                this.setError('No results.');
            }
        },
        setError(msg) {
            this.err = true;
            this.errMsg = msg;
        },
        resetError() {
            this.err = false;
            this.errMsg = '';
        }
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