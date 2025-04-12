<script lang="ts">
    import Assistant from '$lib/components/chat/Assistant.svelte';
</script>

<section class="fixed top-0 left-0 w-full h-screen overflow-hidden py-16 px-4">
  <div class="max-w-6xl mx-auto">
    <div class="text-center mb-8">
      <h1 class="text-4xl font-bold gradient-text mb-4 mt-16">GPT Shield</h1>
      <p class="text-xl text-purple-200 max-w-2xl mx-auto">Your data. Your AI. No Compromises.</p>
    </div>
    
    <div class="relative">
      <Assistant />
    </div>
  </div>
</section> 