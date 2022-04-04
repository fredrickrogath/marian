<template>
  <!-- component -->
  <div class="bg-gray-200 flex items-center justify-center sm:mb-4 mb-2">
    <div class="border-gray-200 w-96 border">
      <!-- <post-card-content v-if="selectedComponent === 'post-card-content'"></post-card-content>
      <comments v-else-if="selectedComponent === 'comments'"></comments> -->

      <transition name="post-comment">
        <component :is="selectedComponent"></component>
      </transition>
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";
import Comments from "@/Jetstream/MyComponents/Comments.vue";
import PostCardContent from "@/Jetstream/MyComponents/PostCardContent.vue";

export default defineComponent({
  components: {
    Comments,
    PostCardContent,
  },
  data() {
    return {
      selectedComponent: "post-card-content",
    };
  },
  props: ['user-name'],

  inject: [],

  provide() {
    return { switchToComments: this.setComments, switchToPost: this.setPost };
  },

  methods: {
    setComments() {
      this.selectedComponent = "comments";
    },
    setPost() {
      this.selectedComponent = "post-card-content";
    },
  },

  watch: {},

  computed: {},
});
</script>

<style scoped>
.post-comment-enter-from {
  opacity: 0;
  transform: translateY(40px);
  height: 0px;
}

.post-comment-enter-active {
  transition: all 0.4 s ease-out;
  height: 0px;
}

.post-comment-enter-to {
  opacity: 1;
  transform: translateY(0);
  height: 0px;
}

.post-comment-leave-from {
  opacity: 1;
  transform: translateY(0);
  height: 0px;
}

.post-comment-leave-active {
  transition: all 0.4s ease-in;
  height: 0px;
  opacity: 1;
}

.post-comment-leave-to {
  opacity: 0;
  transform: translateY(-40px);
  height: 0px;
}

/* .comments {
  height: 690px;
} */
</style>