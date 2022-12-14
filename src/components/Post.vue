<template>
  <div class="container d-flex flex-row">
    <!-- Image -->
    <div>
      <v-img
      :src="post.image"
      height="600"
      width="600"
      contain
    />
    </div>
    <!-- right section -->
    <div class="d-flex flex-column">
      <!-- Right Section Header -->
      <div class="d-flex flex-row justify-space-between">
        <div class="d-flex flex-row card">
          <v-avatar
          width="30"
          height="30"
          >
            <img 
              :src= "post.image"
            />
          </v-avatar>
          <p class="pt-1 text font-weight-medium">{{ post.username }}</p>
        </div>
        <div>
          <p class="font-weight-black">...</p>
        </div>
      </div>
      <hr class="ml-3" >

      <!-- Caption -->
      <div class="d-flex flex-row ml-3 mt-3">
        <p class="font-weight-medium like">{{ post.username }}</p> 
        <p class="pl-1 like">{{ post.caption }}</p>
      </div>

      <!-- Comments -->
      <div 
        v-for="comment in post.Comments" 
        :key="comment.id"
        class="ml-3"
      >
      <p>{{comment}}</p>
        <!-- <p v-for="item in comment">{{ item  }}</p> -->
      </div>

      

      <v-form

      >
        <v-text-field
         placeholder="Add Comment"
         onkeyup=""
         v-model="title"
        >

        </v-text-field>

        <v-btn
          @click="addComment(post.id)"
        >
          add        </v-btn>
      </v-form>
    </div>
    
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
  name: "Post",

  data: () => {
    return{
      title: ""
    }
  },

  methods: {
    increment(post) {
      this.$store.dispatch('increaseLike', post)
    },
    addComment(item) {
      console.log("hey", item)
      if(!this.title) {
        alert("Please add a Comment")
      }

      const newComment = { title: this.title,
        id: item
      }
    console.log("comment",newComment)
      this.$store.dispatch('addComment', newComment)
      
      this.title = ""

    }
  },
  props: {
    post: Object
  }
}
</script>

<style scoped>
.container {
  margin-top: 52px;
  margin-left: 300px;
}

.card {
  margin-right: 18rem;
}
</style>