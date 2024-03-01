<template>
    <div class="admin-dashboard">
      <h2>Admin Dashboard</h2>
      <div class="dashboard-content">
        <!-- Button to add a new venue -->
        <b-button variant="primary" @click="addVenue">+</b-button>
        
        <!-- List of venues -->
        <div v-if="venues.length > 0">
          <h3>Venues</h3>
          <ul>
            <li v-for="venue in venues" :key="venue.id">
              {{ venue.name }}
              <button @click="editVenue(venue)">Edit</button>
              <button @click="removeVenue(venue)">Remove</button>
              <!-- Input fields for specifying ticket price, type, and max attendees -->
              <input type="number" v-model="venue.maxAttendees" placeholder="Max Attendees">
              <input type="number" v-model="venue.ticketPrice" placeholder="Ticket Price">
              <select v-model="venue.ticketType">
                <option value="VIP">VIP</option>
                <option value="Regular">Regular</option>
              </select>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'AdminHomeComponent',
    data() {
      return {
        venues: []
      };
    },
    methods: {
      // Method to add a new venue
      addVenue() {
        const venueName = prompt('Enter venue name:');
        if (venueName) {
          const newVenue = { 
            id: Date.now(), 
            name: venueName,
            maxAttendees: 0, // Initialize max attendees
            ticketPrice: 0, // Initialize ticket price
            ticketType: 'Regular' // Initialize ticket type
          };
          this.venues.push(newVenue);
        }
      },
      // Method to edit a venue
      editVenue(venue) {
        const newName = prompt('Enter new name for the venue:', venue.name);
        if (newName) {
          venue.name = newName;
        }
      },
      // Method to remove a venue
      removeVenue(venue) {
        if (confirm(`Are you sure you want to remove ${venue.name}?`)) {
          const index = this.venues.indexOf(venue);
          if (index !== -1) {
            this.venues.splice(index, 1);
          }
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .admin-dashboard {
    padding: 20px;
  }
  
  .dashboard-content {
    margin-top: 20px;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    margin-bottom: 5px;
  }
  </style>
  