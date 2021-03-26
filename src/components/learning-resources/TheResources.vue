<template>
  <div>
    <base-card>
      <base-button
        :mode="storedResourcesButtonMode"
        @click="setSelectedTab('stored-resources')"
        >Stored Resources
      </base-button>
      <base-button
        :mode="AddResourcesButtonMode"
        @click="setSelectedTab('add-resources')"
      >
        Add Resources
      </base-button>
    </base-card>
    <keep-alive>
      <component :is="selectedTab"></component>
    </keep-alive>
  </div>
</template>
<script>
import StoredResources from "./StoredResources";
import AddResources from "./AddResources";
export default {
  components: {
    StoredResources,
    AddResources,
  },
  data() {
    return {
      selectedTab: "stored-resources",
      storedResources: [
        {
          id: "official-guide",
          title: "Official Guide",
          description: "The official Vue.js documentation",
          link: "https://vuejs.org",
        },
        {
          id: "google-guide",
          title: "Google Guide",
          description: "The Google Vue.js learn",
          link: "https://google.com",
        },
      ],
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.removeResource,
    };
  },
  computed: {
    storedResourcesButtonMode() {
      return this.selectedTab === "stored-resources" ? null : "flat";
    },
    AddResourcesButtonMode() {
      return this.selectedTab === "add-resources" ? null : "flat";
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
      this.storedResources.unshift(newResource);
      this.selectedTab = "stored-resources";
    },
    removeResource(resId) {
      const resIndex = this.storedResources.findIndex((res) => res.id === resId);
      this.storedResources.splice(resIndex, 1);
    },
  },
};
</script>
