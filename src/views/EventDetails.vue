<template>
  <div class="events">
    <h1>{{ event.title }}</h1>
    <div class="event-details">
      <div class="event-details-left">
        <img :src="event.image" alt="event image" />
      </div>
      <div class="event-details-right">
        <p>@ {{ event.time }} on {{ event.date }}</p>
        <p>{{ event.description }}</p>
        <p>{{ event.location }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import EventService from "@/services/EventService.js";
export default {
  name: "EventDetails",
  props: ["id"],
  data() {
    return {
      event: null,
    };
  },
  created() {
    EventService.getEvent(this.id)
      .then((response) => {
        this.event = response.data;
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>

<style scoped>
.events {
  display: flex;
  align-items: center;
  flex-direction: column;
}
.event-details {
  display: flex;
  flex-direction: row;
}
.event-details-left {
  width: 50%;
  height: 300px;
  border: 1px solid #39495c;
}
img {
  width: 100%;
  height: 100%;
  display: block;
}
.event-details-right {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 50%;
  height: 300px;
  border: 1px solid #39495c;
}
</style>