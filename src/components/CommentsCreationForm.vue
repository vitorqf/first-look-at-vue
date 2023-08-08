<script>
  export default {
    name: 'CommentsCreationForm',
    props: {
      comments: Array
    },
    data() {
      return {
        name: "",
        message: ""
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
        this.$emit('new-comment', newComment)

        this.name = ''
        this.message = ''

      }
    },
  }
</script>

<template>
  <!-- Header Section -->
  <div class="flex flex-col gap-1">
        <h1 class="text-2xl font-semibold">Create a new comment</h1>
        <p class="text-zinc-400">Insert your thoughts below to share them with anothers.</p>
      </div>
      
      <!-- Field Section -->
      <div class="flex flex-col gap-2">
        <label for="name" class="tracking-wide">Name</label>
        <input type="text" id="name" name="name" class="px-4 py-3 rounded bg-zinc-700 outline-none focus:ring-2 focus:ring-blue-500" placeholder="Your name" v-model="name"/>
        <small class="text-zinc-400">Empty will be posted as Anonymous</small>
      </div>

      <!-- Field Section -->
      <div class="flex flex-col gap-2">
        <label for="message" class="tracking-wide">Message<span class="text-red-500">*</span></label>
        <textarea type="text" id="message" name="message" class="px-4 py-2 rounded bg-zinc-700 outline-none focus:ring-2 focus:ring-blue-500 resize-none h-[100px]" placeholder="Your message" v-model="message"></textarea>
      </div>

      <!-- Submit Button -->
      <button @click="createNewComment" class="tracking-wider uppercase py-2 px-4 rounded bg-blue-500">Submit</button>
</template>
