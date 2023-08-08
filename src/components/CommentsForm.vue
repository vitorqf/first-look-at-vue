<script>
  import CommentsCreationForm from './CommentsCreationForm.vue';
import CommentsSection from './CommentsSection.vue';

  export default {
    name: 'CommentsForm',
    components: { CommentsCreationForm, CommentsSection },
    data() {
        return {
            comments: [],
        };
    },
    computed: {
        commentsCount() {
            return this.comments.length;
        },
        handleCommentsDefaultName() {
            return this.comments.map(comment => {
                if (!comment.name) {
                    comment.name = 'Anonymous';
                }
                return comment;
            });
        }
    },
    methods: {
      addComment(comment) {
        this.comments.push(comment);
      },
      removeComment(id) {
        this.comments = this.comments.filter(comment => comment.id !== id);
      }
    }
}
</script>

<template>
  <!-- Wrapper -->
  <div class="flex w-[500px]">
    <!-- Container -->
    <div class="bg-zinc-800 border-2 border-zinc-700 rounded-md p-8 flex flex-col gap-4">
      <CommentsCreationForm
        :comments="comments"
        @new-comment="addComment"
      />

      <CommentsSection
        :comments="handleCommentsDefaultName"
        @remove-comment="removeComment"
      />
    </div>
  </div>
</template>




