<template>
    <div>
        <input 
            v-model="searchTerm" 
            placeholder="Search for software..." 
            type="text"
        />
        <ul>
            <li v-for="s in filteredSoftware" :key="s.id">{{ s.name }}</li>
        </ul>
    </div>
</template>

<script>
export default {
    data() {
        return {
            searchTerm: '',
            software: [
                {
                    id: '1',
                    name: 'AVG',
                },
                {
                    id: '2',
                    name: 'AdobeCC',
                },
                {
                    id: '3',
                    name: '7-Zip',
                }
            ],
        };
    },
    computed: {
        filteredSoftware: function() {
            // Filter software
            return this.software.filter(function(s) {
                return s.name.includes(this.searchTerm);
            }.bind(this));
        }
    }
};
</script>