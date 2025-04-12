<script lang="ts">
    // Import any necessary components
    
    // Function to handle extension link clicks
    function handleExtensionClick(browser: string) {
        // In the future, this could redirect to the actual store page
        // For now, just show an alert
        alert(`${browser} extension coming soon!`);
    }
</script>

<section class="py-16 px-4 min-h-screen">
  <div class="max-w-6xl mx-auto">
    <div class="text-center mb-12">
      <h1 class="text-4xl font-bold gradient-text mb-4">Browser Extension</h1>
      <p class="text-xl text-purple-200 max-w-2xl mx-auto">Enhance your development workflow</p>
    </div>
    
    <div class="card-blur p-8 w-full">
      <div class="mb-8 text-center">
        <p class="text-purple-200 mb-6">Install our browser extension to access powerful development tools directly in your browser.</p>
        
        <div class="flex justify-center gap-6 mb-8">
          <button 
            on:click={() => handleExtensionClick('Chrome')}
            class="inline-block px-6 py-3 bg-neon-purple bg-opacity-20 hover:bg-opacity-40 border border-neon-purple text-neon-purple rounded-full transition-all cursor-pointer"
          >
            Chrome Extension
          </button>
          <button 
            on:click={() => handleExtensionClick('Firefox')}
            class="inline-block px-6 py-3 bg-neon-blue bg-opacity-20 hover:bg-opacity-40 border border-neon-blue text-neon-blue rounded-full transition-all cursor-pointer"
          >
            Firefox Add-on
          </button>
        </div>
      </div>
      
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <div class="card-blur p-4">
          <h3 class="text-xl font-semibold text-neon-blue mb-2">Features</h3>
          <ul class="list-disc list-inside text-slate-300 space-y-2">
            <li>Instant code suggestions</li>
            <li>Documentation lookup</li>
            <li>Error detection and fixing</li>
            <li>Performance optimization tips</li>
          </ul>
        </div>
        
        <div class="card-blur p-4">
          <h3 class="text-xl font-semibold text-neon-pink mb-2">Requirements</h3>
          <ul class="list-disc list-inside text-slate-300 space-y-2">
            <li>Chrome 88+ or Firefox 78+</li>
            <li>Active internet connection</li>
            <li>Free account registration</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</section> 