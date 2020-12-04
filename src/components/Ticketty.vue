<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div id="divContent">
      <h2 class="form-label">
        Select an event:
      </h2>
      <p v-for="event in events" :key="event.id">
        <label :for="event.name">
          <img
            :src="event.thumbnailUrl"
            @error="
              $event.target.src =
                'https://designshack.net/wp-content/uploads/placeholder-image-368x246.png'
            "
          />
          <input
            type="radio"
            name="exclusive-event-buttons"
            v-on:click="
              getInstances(
                event.id,
                event.firstInstanceDateTime,
                event.lastInstanceDateTime
              )
            "
            :id="event.id"
            :value="event.name"
            v-model="selectedEvent"
          />
          <span>{{ event.name }}</span>
          <br />
          <span>{{ event.instanceDates }}</span>
          <br />
          <span>Tickets on sale: {{ event.isOnSale }}</span>
        </label>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Ticketty",
  props: {
    msg: String
  },

  data() {
    return {
      events: [],
      selectedEvent: "",
      instances: []
    };
  },

  created() {
    const eventsPromise = this.getEvents();
    eventsPromise.then(data => {
      this.events = data;
    });
  },

  mounted() {},

  computed: {},

  methods: {
    async getEvents() {
      const response = await fetch(
        "http://localhost:8080/apitesting/api/v3/events"
      );

      if (!response.ok) {
        const message = `An error has occured: ${response.status}`;
        throw new Error(message);
      }
      const data = await response.json();
      console.log(data);
      return data;
    },

    async getInstances(eventId, startFrom, startTo) {
      const response = await fetch(
        `http://localhost:8080/apitesting/api/v3/events/${eventId}/instances?start_from=${startFrom}&start_to=${startTo}&interface=4`
      );

      if (!response.ok) {
        const message = `An error has occured: ${response.status}`;
        throw new Error(message);
      }

      const data = await response.json();
      console.log(data);
      // this.instances = data;
      return data;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
img {
  height: 100px;
}
</style>
