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
        handleCommentsDefaultName() {
            return this.comments.map(comment => {
                if (!comment.name) {
                    comment.name = 'Anonymous';
                }
                return comment;
            });
        },
        reversedComments() {
            return this.handleCommentsDefaultName.slice().reverse();
        }
    },
    watch: {
      comments: {
        handler() {
          localStorage.setItem('comments', JSON.stringify(this.comments));
        },
        deep: true
      }
    },
    mounted() {
      if (localStorage.getItem('comments')) {
        this.comments = JSON.parse(localStorage.getItem('comments'));
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
  <div class="flex w-[600px]">
    <!-- Container -->
    <div class="bg-zinc-800 border-2 border-zinc-700 rounded-md p-8 flex flex-col gap-4 w-full">
      <CommentsCreationForm
        :comments="comments"
        @new-comment="addComment"
      />

      <CommentsSection
        :comments="reversedComments"
        @remove-comment="removeComment"
      />

      <footer class="self-center text-zinc-400">
        Designed by <a
          target="_blank"
          referrerpolicy="no-referrer"
          href="https://vitorrafael.com.br"
          class="underline text-white underline-offset-4"
        >Vitor</a>
      </footer>
    </div>
  </div>
</template>




