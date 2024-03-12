<template>
    <div>
        <base-card>
            <base-button @click="setSelectedTap('store-resources')" :mode="storedResButtonMode">Store
                Resources</base-button>
            <base-button @click="setSelectedTap('add-resources')" :mode="addResButtonMode">Add Resources</base-button>
        </base-card>
        <KeepAlive>
            <component :is="selectedTab"></component>
        </KeepAlive>
    </div>
</template>
<script>
import AddResources from './AddResources.vue'
import StoreResources from './StoreResources.vue'
export default {
    components: { StoreResources, AddResources },
    data() {
        return {
            selectedTab: 'store-resources',
            storeResources: [
                {
                    id: 'official-guide',
                    title: 'Official-guide',
                    description: 'The official vue.ks documentation',
                    link: 'https://vuejs.org/guide/quick-start.html#using-vue-from-cdn'
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'The official vue.ks documentation',
                    link: 'https://google.org'
                }
            ]
        }
    },
    provide() {
        return {
            resources: this.storeResources,
            addResource: this.addResource,
            deleteResouces: this.removeResource
        }
    },
    computed: {
        storedResButtonMode() {
            return this.selectedTab === 'store-resources' ? null : 'flat'
        },
        addResButtonMode() {
            return this.selectedTab === 'add-resources' ? null : ' flat';
        }
    },
    methods: {
        setSelectedTap(tab) {
            this.selectedTab = tab
        },
        addResource(title, description, url) {
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: description,
                link: url
            };
            this.storeResources.unshift(newResource)
            this.selectedTab = 'store-resources'
        },
        removeResource(resId) {
            const resIndex = this.storeResources.findIndex(res => res.id === resId)
            this.storeResources.splice(resIndex, 1)
        }
    }
}
</script>