<script setup>
defineProps({
  ticket: {
    type: Object,
    required: true,
  },
})

const emit = defineEmits(['toggle-favourite'])
</script>

<template>
  <article class="card" :class="{ featured: ticket.featured, favourited: ticket.favourite }">
    <div v-if="ticket.featured" class="featured-badge">Featured</div>

    <h2>{{ ticket.name }}</h2>
    <p class="price">R{{ ticket.price }}</p>
    <p class="description">{{ ticket.description }}</p>

    <ul>
      <li v-for="benefit in ticket.benefits" :key="benefit">{{ benefit }}</li>
    </ul>

    <button class="fav-btn" type="button" @click="emit('toggle-favourite', ticket.id)">
      {{ ticket.favourite ? 'Favourited' : 'Favourite' }}
    </button>
  </article>
</template>

<style scoped>
.card {
  border: 2px solid #ddd;
  border-radius: 8px;
  padding: 1.5rem;
  background: #fff;
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  min-height: 390px;
  position: relative;
  transition:
    box-shadow 0.2s,
    transform 0.2s;
}

.card:hover {
  transform: translateY(-4px);
}

.card.featured {
  border-color: #f4a261;
  background: #fff8f0;
  box-shadow: 0 4px 16px rgba(244, 162, 97, 0.3);
}

.card.favourited {
  border-color: #2a9d8f;
}

.featured-badge {
  align-self: flex-start;
  background: #e76f51;
  border-radius: 999px;
  color: #fff;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 1px;
  padding: 0.3rem 0.7rem;
  text-transform: uppercase;
}

h2 {
  font-size: 1.5rem;
  font-weight: 800;
  margin: 0;
  color: #264653;
}

.price {
  font-size: 2rem;
  font-weight: 800;
  color: #e76f51;
  margin: 0;
}

.description {
  color: #555;
  font-size: 0.95rem;
  line-height: 1.5;
  margin: 0;
}

ul {
  padding-left: 1.25rem;
  margin: 0;
  color: #444;
  font-size: 0.92rem;
  line-height: 1.6;
}

.fav-btn {
  margin-top: auto;
  padding: 0.7rem 1rem;
  border: none;
  border-radius: 8px;
  background: #264653;
  color: #fff;
  cursor: pointer;
  font-size: 0.95rem;
  font-weight: 700;
  transition:
    background 0.2s,
    transform 0.2s;
}

.fav-btn:hover {
  background: #2a9d8f;
  transform: translateY(-1px);
}

.favourited .fav-btn {
  background: #2a9d8f;
}
</style>
