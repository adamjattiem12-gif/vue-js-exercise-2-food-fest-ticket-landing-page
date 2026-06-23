<script setup>
import { computed, ref } from 'vue'
import TicketCard from './components/TicketCard.vue'

const tickets = ref([
  {
    id: 1,
    name: 'Bronze',
    price: 150,
    description: 'General admission for a relaxed day of food stalls, live music, and community.',
    benefits: ['Access to all food stalls', 'Live music area', 'Welcome drink'],
    featured: false,
    favourite: false,
  },
  {
    id: 2,
    name: 'Silver',
    price: 300,
    description: 'The best value tier with faster entry and extra festival experiences.',
    benefits: ['Everything in Bronze', 'Priority entry', 'Chef demo access', 'Goodie bag'],
    featured: true,
    favourite: false,
  },
  {
    id: 3,
    name: 'Gold',
    price: 500,
    description: 'A VIP festival pass for guests who want premium comfort and exclusive access.',
    benefits: ['Everything in Silver', 'VIP lounge access', 'Meet and greet', 'Premium seating'],
    featured: false,
    favourite: false,
  },
])

const favouriteCount = computed(() => tickets.value.filter((ticket) => ticket.favourite).length)

function toggleFavourite(id) {
  const ticket = tickets.value.find((item) => item.id === id)
  if (ticket) {
    ticket.favourite = !ticket.favourite
  }
}
</script>

<template>
  <div class="page">
    <header class="site-header">
      <p class="eyebrow">Outdoor food festival</p>
      <h1>Cape Town Food Fest 2025</h1>
      <p class="intro">
        A weekend of local chefs, street vendors, live music, and community. Compare the ticket
        tiers and favourite the one you would choose.
      </p>
      <p class="favourite-summary">
        {{ favouriteCount }} {{ favouriteCount === 1 ? 'tier' : 'tiers' }} favourited
      </p>
    </header>

    <main class="ticket-grid">
      <TicketCard
        v-for="ticket in tickets"
        :key="ticket.id"
        :ticket="ticket"
        @toggle-favourite="toggleFavourite"
      />
    </main>

    <footer class="site-footer">
      <p>&copy; 2025 Cape Town Food Fest. All rights reserved.</p>
    </footer>
  </div>
</template>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family:
    Inter, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
  background: #f7f3ed;
  color: #1f2933;
}

.page {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.site-header {
  background:
    linear-gradient(rgba(29, 53, 87, 0.78), rgba(29, 53, 87, 0.78)),
    url('https://images.unsplash.com/photo-1555939594-58d7cb561ad1?auto=format&fit=crop&w=1600&q=80');
  background-position: center;
  background-size: cover;
  color: #fff;
  text-align: center;
  padding: 4rem 1.25rem 3.5rem;
}

.eyebrow {
  color: #f4a261;
  font-size: 0.78rem;
  font-weight: 800;
  letter-spacing: 0.14em;
  margin-bottom: 0.75rem;
  text-transform: uppercase;
}

.site-header h1 {
  font-size: clamp(2.4rem, 6vw, 4.6rem);
  font-weight: 900;
  line-height: 1;
  margin-bottom: 1rem;
}

.intro {
  font-size: 1.05rem;
  line-height: 1.7;
  margin: 0 auto;
  max-width: 680px;
  opacity: 0.92;
}

.favourite-summary {
  background: rgba(255, 255, 255, 0.16);
  border: 1px solid rgba(255, 255, 255, 0.28);
  border-radius: 999px;
  display: inline-flex;
  font-weight: 700;
  margin-top: 1.5rem;
  padding: 0.55rem 1rem;
}

.ticket-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1.5rem;
  padding: 2.5rem 1.5rem;
  max-width: 1100px;
  margin: 0 auto;
  width: 100%;
}

.site-footer {
  margin-top: auto;
  text-align: center;
  padding: 1.5rem;
  background: #264653;
  color: rgba(255, 255, 255, 0.7);
  font-size: 0.85rem;
}

@media (max-width: 640px) {
  .site-header {
    padding: 3.25rem 1rem 2.75rem;
  }

  .ticket-grid {
    grid-template-columns: 1fr;
    padding: 2rem 1rem;
  }
}
</style>
