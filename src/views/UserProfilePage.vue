<template>
  <div>
    <UserNavBarComponent></UserNavBarComponent>
    <!-- Your template content goes here -->
  </div>
</template>

<script>
import UserNavBarComponent from '@/components/UserNavBarComponent.vue'; // Adjust the import path as per your project structure

export default {
  name: "UserProfilePage",
  components: {
    UserNavBarComponent,
  },
  methods: {
    // Your methods go here
  },
};
</script>
