<script>
  import CommentsCreationForm from './CommentsCreationForm.vue';

  export default {
    name: 'CommentsForm',
    data() {
        return {
            comments: [],
        };
    },
    methods: {
      addComment(comment) {
        this.comments.push(comment);
      },
      removeComment(id) {
        this.comments = this.comments.filter(comment => comment.id !== id);
      }
    },
    computed: {
        commentsCount() {
            return this.comments.length;
        },
        commentsWithNoName() {
            return this.comments.map(comment => {
                if (!comment.name) {
                    comment.name = 'Anonymous';
                }
                return comment;
            });
        }
    },
    components: { CommentsCreationForm }
}
</script>

<template>
  <!-- Wrapper -->
  <div class="flex w-[500px]">

    <!-- Container -->
    <div class="bg-zinc-800 border-2 border-zinc-700 rounded-md p-8 flex flex-col gap-4">
      <CommentsCreationForm @new-comment="addComment" :comments="comments"/>

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




