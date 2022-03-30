<template>
  <app-layout title="Dashboard">
    <div class="py-2">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="overflow-hidden shadow-xl sm:rounded-lg overflow-auto">
          <div class="flex flex-wrap justify-evenly sm:my-2">
            <keep-alive>
            <post-card
              v-for="user in users"
              :key="user.id"
              :user-name="user.name"
            ></post-card>
            </keep-alive>
          </div>
        </div>
      </div>
    </div>
  </app-layout>
</template>

<script>
import { defineComponent } from "vue";
import AppLayout from "@/Layouts/AppLayout.vue";
import Welcome from "@/Jetstream/Welcome.vue";
import PostCard from "@/Jetstream/MyComponents/PostCard.vue";

export default defineComponent({
  components: {
    AppLayout,
    Welcome,
    PostCard,
  },
  data() {
    return {
      users: [],
      loadUsers: true,
      url: 'https://dummyjson.com/products',
    };
  },
  beforeMount() {
    if(this.loadUsers){
      this.fetchUsers();
    }
  },
  mounted() {
    // this.getNextUser();
    this.loadUsers = false;
  },
  methods: {
    fetchUsers() {

        fetch('https://dummyjson.com/products/')
.then(res => res.json())
.then(json => {this.users = json.products;console.log('used again')})

      // POST request using fetch with error handling
    //   const requestOptions = {
    //     method: "GET",
    //     headers: {
    //       "Content-Type": "application/json",
    //       Authorization: "Bearer 1|H1OrjYLqsPL92YYs9FNjsB311IL9riHIzx0gzL9y",
    //     },
    //     // body: JSON.stringify({ title: 'Vue POST Request Example' })
    //   };
    //   fetch( this.url, requestOptions)
    //     .then(async (response) => {
    //       const data = await response.json();
    //       this.users = data.data;
    //     //   console.log(data.data);

    //       // check for error response
    //       if (!response.ok) {
    //         // get error message from body or default to response status
    //         const error = (data && data.message) || response.status;
    //         return Promise.reject(error);
    //       }

    //       // this.postId = data.id;
    //     })
    //     .catch((error) => {
    //       this.errorMessage = error;
    //       console.error("There was an error!", error);
    //     });
    },getNextUser() {
      window.onscroll = () => {
        let bottomOfWindow = document.documentElement.scrollTop + window.innerHeight === document.documentElement.offsetHeight;
        if (bottomOfWindow) {
          axios.get( this.url).then(response => {
            this.users.push(response.data.results[0]);
          });
        }
      }
    }
  },
});
</script>


<style>
@import './../../../public/css/app.css';
</style>