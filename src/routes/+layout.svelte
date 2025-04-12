<script lang="ts">
    import '../app.css'; // Import Tailwind styles
  </script>
  
  <nav class="navbar-blur py-4 px-6">
    <div class="max-w-6xl mx-auto flex justify-between items-center">
      <div class="flex items-center space-x-2">
        <span class="text-2xl font-bold gradient-text glow">Layer8</span>
        <span class="text-purple-300">AI</span>
      </div>
      <div class="hidden md:flex space-x-6">
        <a href="/" class="text-purple-200 hover:text-neon-purple transition-colors">Home</a>
        <a href="/docs" class="text-purple-200 hover:text-neon-purple transition-colors">Documentation</a>
        <a href="/about" class="text-purple-200 hover:text-neon-purple transition-colors">About</a>
      </div>
    </div>
  </nav>
  
  <main class="pt-20">
    <slot />
  </main>
  