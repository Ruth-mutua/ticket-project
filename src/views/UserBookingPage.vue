<template>
    <div>
      <UserNavBarComponent></UserNavBarComponent>
  
      <div class="container">
        <h2>User Booking Page</h2>
  
        <!-- Display Available Movies -->
        <div v-for="movie in movies" :key="movie.id" class="movie-card">
          <h3>{{ movie.title }}</h3>
          <p>Start Time: {{ movie.start_timing }}</p>
          <p>End Time: {{ movie.end_timing }}</p>
          <p>Available Seats: {{ movie.available_seats }}</p>
          <button @click="bookMovie(movie.id)">Book Now</button>
        </div>
  
        <!-- Display Booking Form -->
        <b-modal v-model="showBookingModal" title="Book Movie" hide-footer>
          <form @submit.prevent="confirmBooking">
            <b-form-group label="Name">
              <b-form-input v-model="booking.name" required></b-form-input>
            </b-form-group>
            <b-form-group label="Email">
              <b-form-input type="email" v-model="booking.email" required></b-form-input>
            </b-form-group>
            <b-button type="submit" variant="primary">Confirm Booking</b-button>
          </form>
        </b-modal>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: "UserBookingPage",
    data() {
      return {
        movies: [],
        showBookingModal: false,
        selectedMovieId: null,
        booking: {
          name: '',
          email: ''
        }
      };
    },
    mounted() {
      this.fetchMovies();
    },
    methods: {
      async fetchMovies() {
        const response = await axios.get('http://localhost:5000/movies');
        this.movies = response.data;
      },
      bookMovie(movieId) {
        this.selectedMovieId = movieId;
        this.showBookingModal = true;
      },
      async confirmBooking() {
        try {
          await axios.post(`http://localhost:5000/bookings`, {
            movieId: this.selectedMovieId,
            name: this.booking.name,
            email: this.booking.email
          });
          // Optionally, you can perform additional actions after booking confirmation
          // For example, show a success message or redirect to a confirmation page
          console.log('Booking confirmed');
          // Reset booking data and modal state
          this.booking = {
            name: '',
            email: ''
          };
          this.showBookingModal = false;
        } catch (error) {
          console.error('Error confirming booking:', error);
          // Optionally, handle booking errors, show error messages, etc.
        }
      }
    },
  };
  </script>
  
  <style scoped>
  .container {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
  }
  
  .movie-card {
    background-color: #f9f9f9;
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 15px;
    margin-bottom: 20px;
  }
  
  .movie-card h3 {
    margin-top: 0;
  }
  
  .movie-card p {
    margin-bottom: 5px;
  }
  
  .movie-card button {
    background-color: #007bff;
    color: #fff;
    border: none;
    padding: 8px 16px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .movie-card button:hover {
    background-color: #0056b3;
  }
  
  /* Modal Styles */
  .modal-content {
    max-width: 400px;
    margin: 0 auto;
  }
  
  .modal-footer {
    display: flex;
    justify-content: flex-end;
  }
  
  /* Form Styles */
  .b-form-group {
    margin-bottom: 20px;
  }
  
  .b-form-input {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }
  
  .b-button[type="submit"] {
    background-color: #007bff;
    color: #fff;
    border: none;
    padding: 8px 16px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .b-button[type="submit"]:hover {
    background-color: #0056b3;
  }
  </style>
  