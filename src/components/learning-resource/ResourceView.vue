<template>
  <BaseCard>
    <BaseButton
      @click="setSelectedTab('StoredResource')"
      :mode="storeResButtonMode"
      >Stored Resources</BaseButton
    >
    <BaseButton @click="setSelectedTab('AddResource')" :mode="addResButtonMode"
      >Add Resource</BaseButton
    >
  </BaseCard>
  <KeepAlive> <Component :is="selectedTab"></Component></KeepAlive>
</template>

<script>
import AddResource from './AddResource.vue';
import StoredResource from './StoredResource.vue';

export default {
  components: { AddResource, StoredResource },
  data() {
    return {
      selectedTab: 'StoredResource',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to Google',
          link: 'https://google.com',
        },
      ],
    };
  },
  computed: {
    storeResButtonMode() {
      return this.selectedTab === 'StoredResource' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'AddResource' ? null : 'flat';
    },
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.deleteResource,
    };
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(resource) {
      this.storedResources.unshift(resource);
      this.selectedTab = 'StoredResource';
    },
    deleteResource(id) {
      const index = this.storedResources.findIndex((el) => el.id === id);
      this.storedResources.splice(index, 1);
    },
  },
};
</script>
