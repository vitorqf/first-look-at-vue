<script>
  export default {
    name: 'CommentsSection',
    props: {
      comments: {
        type: Array,
        default: () => []
      }
    }, 
    methods: {
      removeComment(id) {
        this.$emit('remove-comment', id)
      }
    },
  }
</script>

<template>
  <!-- Comments Section -->
  <div>
    <!-- Header Section -->
    <div class="flex flex-col gap-1 mb-2">
      <h2 class="text-2xl font-semibold">
        Comments
      </h2>
      <p
        v-if="comments.length == 0"
        class="text-zinc-400"
      >
        No comments yet.
      </p>
    </div>

    <!-- Comments -->
    <div class="flex flex-col gap-4 max-h-[350px] pr-0.5 overflow-y-auto">
      <!-- Comment -->
      <div
        v-for="comment in comments"
        :key="comment.id"
        class="flex flex-col gap-2 bg-zinc-800 border-2 border-zinc-700 p-4 rounded-md"
      >
        <!-- User Info + Date -->
        <div class="flex justify-between items-center">
          <h3 class="text-lg font-semibold">
            {{ comment.name }}
          </h3>
          <p class="text-zinc-400 text-sm">
            {{ comment.createdAt }}
          </p>
        </div>

        <!-- Message -->
        <p class="text-zinc-400 text-justify break-words">
          {{ comment.message }}
        </p>
        <button
          class="text-sm text-red-500 self-start"
          @click="removeComment(comment.id)"
        >
          Remove
        </button>
      </div>
    </div>
  </div>
</template>
