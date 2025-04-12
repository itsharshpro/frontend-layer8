<script lang="ts">
    import Assistant from '$lib/components/chat/Assistant.svelte';
</script>

<section class="py-16 px-4 min-h-screen">
  <div class="max-w-6xl mx-auto">
    <div class="text-center mb-8">
      <h1 class="text-4xl font-bold gradient-text mb-4">AI Assistant</h1>
      <p class="text-xl text-purple-200 max-w-2xl mx-auto">Get intelligent answers to your programming questions</p>
    </div>
    
    <div class="relative">
      <Assistant />
    </div>
  </div>
</section> 