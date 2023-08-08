<script>
  export default {
    name: 'CommentsSection',
    data() {
      return {
        comments: [],
        name: '',
        message: ''
      }
    },
    methods: {
      createNewComment() {
        if (!this.message) {
          return alert('Please insert a message')
        }

        const newComment = {
          id: this.comments.length + 1,
          name: this.name,
          message: this.message,
          createdAt: new Date().toLocaleDateString()
        }
        this.comments.push(newComment)
        this.name = ''
        this.message = ''
      },

      removeComment(id) {
        this.comments = this.comments.filter(comment => comment.id !== id)
      }
    },
    computed: {
      commentsCount() {
        return this.comments.length
      },
      commentsWithNoName() {
        return this.comments.map(comment => {
          if (!comment.name) {
            comment.name = 'Anonymous'
          }
          return comment
        })
      }
    }
  }
</script>

<template>
  <!-- Wrapper -->
  <div class="flex w-[500px]">

    <!-- Container -->
    <div class="bg-zinc-800 border-2 border-zinc-700 rounded-md p-8 flex flex-col gap-4">
      <!-- Header Section -->
      <div class="flex flex-col gap-1">
        <h1 class="text-2xl font-semibold">Create a new comment</h1>
        <p class="text-zinc-400">Insert your thoughts below to share them with anothers.</p>
      </div>
      
      <!-- Field Section -->
      <div class="flex flex-col gap-2">
        <label for="name">Name</label>
        <input type="text" id="name" name="name" class="px-4 py-3 rounded bg-zinc-700 outline-none focus:ring-2 focus:ring-blue-500" placeholder="Your name" v-model="name"/>
        <small class="text-zinc-400">Empty will be posted as Anonymous</small>
      </div>

      <!-- Field Section -->
      <div class="flex flex-col gap-2">
        <label for="message">Message</label>
        <textarea type="text" id="message" name="message" class="px-4 py-2 rounded bg-zinc-700 outline-none focus:ring-2 focus:ring-blue-500 resize-none h-[100px]" placeholder="Your message" v-model="message"></textarea>
      </div>

      <!-- Submit Button -->
      <button @click="createNewComment" class="tracking-wider uppercase py-2 px-4 rounded bg-blue-500">Submit</button>

      <!-- Comments Section -->
      <div>
        <!-- Header Section -->
        <div class="flex flex-col gap-1 mb-2">
          <h2 class="text-2xl font-semibold">Comments</h2>
          <p class="text-zinc-400 text-sm">Total: {{ commentsCount }}</p>
        </div>

        <!-- Comments -->
        <div class="flex flex-col gap-4 max-h-[200px] overflow-y-auto">

          <!-- Comment -->
          <div class="flex flex-col gap-2 bg-zinc-700 px-4 py-2 rounded-md" v-for="comment in commentsWithNoName" v-bind:key="comment.id">

            <!-- User Info + Date -->
            <div class="flex justify-between items-center">
              <h3 class="text-lg font-semibold">{{ comment.name }}</h3>
              <p class="text-zinc-400 text-sm">{{ comment.createdAt }}</p>
            </div>

            <!-- Message -->
            <p class="text-zinc-400 max-w-[426px] break-words">{{ comment.message }}</p>
            <button @click="removeComment(comment.id)" class="text-sm text-red-500 self-start">Remove</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>




