<template>
    
    <base-card>
        <base-button 
            @click="setSelectedTab('stored-resources')"
            :mode="storedResButtonMode"
        >Stored Resoureces</base-button>
        <base-button 
            @click="setSelectedTab('add-resources')"
            :mode="addResButtonMode"
        >Add Resoureces</base-button>
    </base-card>

    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>

</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResources from './AddResource.vue';




export default {
    components: {        
        'stored-resources': StoredResources,
        'add-resources': AddResources,
    },
    data() {
        return {
            selectedTab: 'stored-resources',
            storedResources: [
                {
                    id: 'official-guide',
                    title: 'Vue Official Guide',
                    description: 'The official Vue.js documentaion',
                    link: 'https://vuejs.org'
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'Need to know how to google yours information',
                    link: 'https://google.com'
                },
            ],
        };
    },
    computed: {
        storedResButtonMode() {
            return this.selectedTab === 'stored-resources' ? null : 'flat';
        },
        addResButtonMode() {
            return this.selectedTab === 'add-resources' ? null : 'flat';
        },
    },
    provide() {
        return {
            resources: this.storedResources,
            addResource: this.addResource,
            removeResource: this.removeResource,
        }
    },
    methods: {
        setSelectedTab(tab) {
            this.selectedTab = tab;
        },
        addResource(title, description, url) {
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: description,
                link: url,
            }
            this.storedResources.unshift(newResource);
            this.selectedTab = 'stored-resources';
        },
        removeResource(id) {
            const resourceIdx = this.storedResources.findIndex((res) => res.id === id);
            this.storedResources.splice(resourceIdx, 1);
        }

    }
}
</script>