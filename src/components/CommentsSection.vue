<script>
  export default {
    name: 'CommentsSection',
  }
</script>

<template>
  <div class="flex w-[500px]">
    <form class="bg-zinc-800 border-2 border-zinc-700 rounded-md p-8 flex flex-col gap-4">
      <div class="flex flex-col gap-1">
        <h1 class="text-3xl font-semibold self-start">Comments</h1>
        <p class="text-zinc-400">Insert your thoughts below to share them with anothers.</p>
      </div>
      
      <div class="flex flex-col gap-2">
        <label for="name">Name</label>
        <input type="text" id="name" name="name" class="px-4 py-3 rounded bg-zinc-700 outline-none focus:ring-2 focus:ring-blue-500" placeholder="Your name"/>
      </div>

      <div class="flex flex-col gap-2">
        <label for="message">Message</label>
        <textarea type="text" id="message" name="message" class="px-4 py-2 rounded bg-zinc-700 outline-none focus:ring-2 focus:ring-blue-500 resize-none h-[100px]" placeholder="Your message"></textarea>
      </div>
      <button type="submit" class="tracking-wider uppercase py-2 px-4 rounded bg-blue-500">Submit</button>
    </form>
  </div>
</template>




