<template>
    <div class="user-home">
      <h2>Event Details</h2>
      <div v-if="event" class="event-details">
        <p><strong>Name:</strong> {{ event.name }}</p>
        <p><strong>Ticket Price:</strong> {{ event.ticketPrice }}</p>
        <p><strong>Maximum Attendees:</strong> {{ event.maxAttendees }}</p>
      </div>
      
      <h2>Reserve Tickets</h2>
      <form @submit.prevent="reserveTickets" class="reservation-form">
        <label for="ticketQuantity">Number of Tickets (max 5):</label>
        <input type="number" id="ticketQuantity" v-model="ticketQuantity" min="1" max="5" required>
        <button type="submit">Reserve</button>
      </form>
      
      <!-- Display success message or error message -->
      <p v-if="reservationSuccess" class="success-message">Reservation successful. You will receive an email notification.</p>
      <p v-if="reservationError" class="error-message">Reservation failed. Please try again.</p>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: "UserHomeComponent",
    data() {
      return {
        event: null,
        ticketQuantity: 1,
        reservationSuccess: false,
        reservationError: false
      };
    },
    created() {
      // Fetch event details (You need to implement this)
      this.fetchEventDetails();
    },
    methods: {
      fetchEventDetails() {
        async fetchEventDetails() {
      try {
        const response = await axios.get('api/event-details'); // Adjust URL based on your backend API endpoint
        this.event = response.data; // Assuming the response contains the event details object
      } catch (error) {
        console.error('Error fetching event details:', error);
      }
    },
      async reserveTickets() {
        // Implement logic to reserve tickets
        // Check if the ticketQuantity is valid
        if (this.ticketQuantity <= 0 || this.ticketQuantity > 5) {
          return; // Exit if the quantity is invalid
        }
        
        try {
        // Make API call to reserve tickets
        const response = await axios.post('api/reserve-tickets', {
          eventId: this.event.id,
          quantity: this.ticketQuantity
        });
        // Handle successful reservation
        this.reservationSuccess = true;
        // Send email notification
        this.sendEmailNotification();
      } catch (error) {
        // Handle reservation error
        console.error('Reservation failed:', error);
        this.reservationError = true;
      }
    }},
    async sendEmailNotification() {
      try {
        // Make API call to send email notification
        await axios.post('api/send-email-notification', {
          eventId: this.event.id,
          userEmail: 'user@example.com' // Assuming you have the user's email address
        });
        console.log('Email notification sent successfully');
      } catch (error) {
        console.error('Error sending email notification:', error);
      }
    }
  } 
};

</script>

  
  <style scoped>
  .user-home {
    padding: 20px;
  }
  
  .event-details {
    margin-bottom: 20px;
  }
  
  .reservation-form {
    margin-bottom: 20px;
  }
  
  .success-message {
    color: green;
  }
  
  .error-message {
    color: red;
  }
  </style>
  