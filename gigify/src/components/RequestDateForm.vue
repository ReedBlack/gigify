<template>
 <div id="backgroundForm">
     <div id="request">
       <h1>Request to be added to event</h1>
       <form
         class="requestForm"
         :submitRequest="submitRequest"
         v-on:submit.prevent="submitRequest"
       >
         <input
           v-model="request.date"
           class="form-control mb-2 mr-sm-2"
           type="text"
           name="date"
           :placeholder=showDate
           readonly
         >
         <input
           v-model="request.artist"
           class="form-control mb-2 mr-sm-2"
           type="text"
           name="artistName"
           placeholder="Artist Name"
         >
         <input
           v-model="request.contactName"
           class="form-control mb-2 mr-sm-2"
           type="text"
           name="contactName"
           placeholder="Contact Name"
         >
         <input
           v-model="request.phone"
           class="form-control mb-2 mr-sm-2"
           type="text"
           name="phone"
           placeholder="Phone Number"
         >
         <input
           v-model="request.email"
           class="form-control mb-2 mr-sm-2"
           type="text"
           name="email"
           placeholder="Email"
         >
         <input
           v-model="request.website"
           class="form-control mb-2 mr-sm-2"
           type="text"
           name="website"
           placeholder="Website"
         >
         <input
           v-model="request.musicSample"
           class="form-control mb-2 mr-sm-2"
           type="text"
           name="phone"
           placeholder="Embed link from YouTube or SoundCloud"
         >
         <input
           v-model="request.image"
           class="form-control mb-2 mr-sm-2"
           type="text"
           name="image"
           placeholder="Image (Link directly to a publicly accessible promo shot)"
         >         
         <input
           v-model="request.description"
           name="description"
           class="form-control mb-2 mr-sm-2"
           placeholder="Short Artist Description">
         <input
           type="submit"
           id="submitButton"
           name="submit"
           value="Submit"
         />
     </form>
         <footer>
             <button
               id="return"
               @click.prevent="toggleDisplay"
               class="btn"
             >
               Go back to available dates
             </button>
         </footer>
     </div>
   </div>
</template>

<script>
export default {
  name: "request-date-form",
  props: ["isDisplaying", "toggleDisplay", "API", "showDate"],
  data() {
    return {
      request: {
        date: "",
        artist: "",
        contactName: "",
        phone: "",
        email: "",
        website: "",
        musicSample: "",
        image: "",
        description: ""
      }
    };
  },
  methods: {
    submitRequest() {
      this.request.date = this.showDate;
      this.postRequest();
      this.request = {
        date: "",
        artist: "",
        contactName: "",
        phone: "",
        email: "",
        website: "",
        musicSample: "",
        image: "",
        description: ""
      };
    },
    postRequest() {
      const postOptions = {
        method: "POST",
        body: JSON.stringify(this.request),
        headers: { "Content-Type": "application/json" }
      };
      fetch(this.API.REQUESTED_SHOWS, postOptions)
        .then(res => res.json())
        .then(resJSON => console.log(resJSON));
    }
  }
};
</script>

<style scoped>
#submitButton {
  font-size: 25px;
  margin: 40px;
  border-radius: 300px;
  background-color: #f88c19;
  color: white;
  width: 50%;
}
#request {
  background-color: RGB(70, 68, 68);
  padding: 1% 2% 2% 2%;
  margin-top: 5%;
  width: 50%;
}
#backgroundForm {
  display: flex;
  justify-content: center;
  background-color: transparent;
}

h1 {
  color: white;
}

@media only screen and (max-width: 600px) {
  #request {
    width: 90%;
  }
}
</style>