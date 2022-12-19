<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResButton"
      >Stored Resources
    </base-button>

    <base-button @click="setSelectedTab('add-resource')" :mode="addResButton">
      Add Resource
    </base-button>
  </base-card>
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
    AddResource,
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      storeResources: [
        {
          id: 'offical-guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentaion',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to google...',
          link: 'https://google.org',
        },
      ],
    };
  },
  provide() {
    return {
      resources: this.storeResources,
      theResource: this.addResource,
      deleteItems: this.removeItems,
    };
  },
  computed: {
    storedResButton() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButton() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
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
      };
      this.storeResources.unshift(newResource);
      this.selectedTab = 'stored-resources';
    },

    removeItems(resId) {
      const resIndex = this.storeResources.findIndex((res) => res.id === resId);
      this.storeResources.splice(resIndex, 1);
    },
  },
};
</script>
