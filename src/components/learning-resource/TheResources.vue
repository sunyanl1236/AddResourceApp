<template>
    <base-card>
    <!-- we can add props or event listeners on custom components, then by default they fall through to the root level element
    in that custom components template. If add click event listener in base-button, it will fall through and will be applied to <button> in BaseButton. 
    -->
        <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored Resources</base-button>
        <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMode">Add Resource</base-button>
    </base-card>
    <!-- keep the input, not lose input -->
    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
    components: {
        StoredResources,
        AddResource
    },
    data(){
        return {
            selectedTab: 'stored-resources',
            storedResources: [
                {
                id: 'Official guide',
                title: 'Official guide',
                description: 'The Official Vue.js documentation.',
                link: 'https://vuejs.org'
                },
                {
                id: 'google',
                title: 'google',
                description: 'Learn to google.',
                link: 'https://google.org'
                }
            ],
        };
    },
    provide() {
        return {
            resources: this.storedResources,
            addResource: this.addResource,
            deleteResource: this.removeResource
        };
    },
    computed: {
        storedResButtonMode() {
            return this.selectedTab === 'stored-resources'? null : 'flat';
        },
        addResButtonMode() {
            return this.selectedTab === 'add-resource'? null : 'flat';
        }
    },
    methods: {
        setSelectedTab(tab){
            this.selectedTab = tab;
        },
        addResource(title, description, url) {
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: description,
                link: url
            };
            this.storedResources.unshift(newResource);
            this.selectedTab = 'stored-resources';
        },
        removeResource(resId) {
            /*
            method 1: use filter() to delete, not working
            provide() actually provide the reference of storedResources to all components have 'inject'
            so all components 'inject' storedResources have the reference point to the same storedResources array
            but filter() will return a new reference, thus all components still use to the old reference, not newly returned reference
            */
            // this.storedResources = this.storedResources.filter(res => res.id != resId);

            //method 2: remove unmutably, use splice() to manipulate original array 
            const resIndex = this.storedResources.findIndex(res => res.id === resId);
            this.storedResources.splice(resIndex, 1);
        }
    }
}
</script>