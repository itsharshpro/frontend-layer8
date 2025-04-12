<script lang="ts">
    import Assistant from '$lib/components/chat/Assistant.svelte';
</script>

<section id="chat-assistant" class="py-20 px-4">
  <div class="max-w-6xl mx-auto">
    <h2 class="text-5xl font-bold text-center mb-10">
      Your <span class="gradient-text glow">Secure</span> AI Assistant
    </h2>
    <div class="relative">
      <div class="absolute -top-16 -left-16 w-32 h-32 bg-neon-purple rounded-full filter blur-3xl opacity-20"></div>
      <div class="absolute -bottom-16 -right-16 w-32 h-32 bg-neon-blue rounded-full filter blur-3xl opacity-20"></div>
      <Assistant />
    </div>
  </div>
</section>
  