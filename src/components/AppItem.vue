  <template>
    <div class="col-3">
    <router-link :to="{ path: '/' }"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-house-fill" viewBox="0 0 16 16">
    <path fill-rule="evenodd" d="m8 3.293 6 6V13.5a1.5 1.5 0 0 1-1.5 1.5h-9A1.5 1.5 0 0 1 2 13.5V9.293l6-6zm5-.793V6l-2-2V2.5a.5.5 0 0 1 .5-.5h1a.5.5 0 0 1 .5.5z"/>
    <path fill-rule="evenodd" d="M7.293 1.5a1 1 0 0 1 1.414 0l6.647 6.646a.5.5 0 0 1-.708.708L8 2.207 1.354 8.854a.5.5 0 1 1-.708-.708L7.293 1.5z"/>
    </svg> Back Home</router-link>
    </div>
    <h2 class="text-primary">{{ $route.params.name }}</h2>
    <h3>Rate Beer <span class="text-info">{{ picked }}</span></h3>
    <div class="row mb-3 align-items-center">
      <form v-on:submit.prevent="submitForm($route.params.id)">
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="radio" id="1" value="1" v-model="picked" />
        <label for="1">1</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="radio" id="2" value="2" v-model="picked" />
        <label for="2">2</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="radio" id="3" value="3" v-model="picked" />
        <label for="3">3</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="radio" id="4" value="4" v-model="picked" />
        <label for="4">4</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="radio" id="5" value="5" v-model="picked" />
        <label for="5">5</label>
      </div>
      <div class="row">
        <div class="centered">
          <div class="form-group">
            <label for="textarea1">Add Comment</label>
            <textarea v-model="comments" class="form-control" id="textarea1" rows="3" placeholder="Write something here..."></textarea>
          </div>
        </div>
      </div>
      <div class="form-group">
        <button class="btn btn-primary">Submit</button>
      </div>
      </form>
    </div>
  </template>

<script>
/* eslint-disable */
import axios from 'axios';
import constants from "@/components/constants";

export default {
  data() {
    return {
        picked: '5',
        comment: '',
        id: ''
    }
  },
  methods: {
    submitForm(id) {
      let axiosConfig = {
        headers: { "x-user": constants.API_EMAIL }
      };
      let postData = {
            id: id,
            rating: this.picked,
            comments: this.comments
      };
      axios.post(constants.API_URL + '/rating/', postData, axiosConfig)
          .then((res) => {
                     if (res.data == 'SUCCESS') alert('Rating was added.');
                 })
                 .catch((error) => {
                     // error.response.status Check status code
                 }).finally(() => {
                     //Perform action in always
                 });
    },
    hasHistory () { return window.history.length > 2 }
  }
}
</script>
<style>
.centered {
  float: none;
  margin: 2rem auto;
  width: 50rem;
}
</style>
