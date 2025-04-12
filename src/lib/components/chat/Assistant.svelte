<script lang="ts">
    import { onMount } from 'svelte';
  
    let query = '';
    let messages = [];
    let isLoading = false;
    let error: string | null = null;
    let thinkingInfo: {
      original: string;
      anonymized: string;
      report: string;
    } | null = null;
  
    const API_URL = 'http://localhost:8000';
    const DEFAULT_PROVIDER = 'gemini';
    const DEFAULT_MODEL = 'gemini-2.0-flash';
    const DEFAULT_TEMPERATURE = 0.7;
    const DEFAULT_MAX_TOKENS = 1000;
  
    onMount(() => {
      messages = [
        {
          role: 'assistant',
          content:
            "Hello! I'm your secure AI assistant. Your queries will be anonymized before processing to protect sensitive information. How can I help you today?"
        }
      ];
    });
  
    async function sendQuery() {
      if (!query.trim()) return;
  
      const userMessage = query;
      query = '';
  
      messages = [...messages, { role: 'user', content: userMessage }];
      isLoading = true;
      error = null;
      thinkingInfo = null;
  
      try {
        const encodedQuery = encodeURIComponent(userMessage);
        const url = `${API_URL}/query/${encodedQuery}?provider=${DEFAULT_PROVIDER}&model=${DEFAULT_MODEL}&temperature=${DEFAULT_TEMPERATURE}&max_tokens=${DEFAULT_MAX_TOKENS}`;
  
        const response = await fetch(url);
        if (!response.ok) throw new Error(`API returned status ${response.status}`);
  
        const data = await response.json();
  
        // Temporary anonymization display
        thinkingInfo = {
          original: data.original_query,
          anonymized: data.anonymized_query,
          report: data.formatted_report
        };
  
        // Simulate brief "thinking" delay
        await new Promise((resolve) => setTimeout(resolve, 5000));
  
        // Final assistant response
        messages = [
          ...messages,
          {
            role: 'assistant',
            content: data.deanonymized_response
          }
        ];
      } catch (err: any) {
        console.error('Error calling API:', err);
        error = `Error: ${err.message}. Make sure the API server is running at ${API_URL}.`;
      } finally {
        isLoading = false;
        thinkingInfo = null;
      }
    }
  
    function handleKeydown(event: KeyboardEvent) {
      if (event.key === 'Enter' && !event.shiftKey) {
        event.preventDefault();
        sendQuery();
      }
    }
  </script>
  
  <!-- Improved UI with blur effects -->
  <div class="blur-panel rounded-xl shadow-2xl overflow-hidden backdrop-blur-lg">
  
    <!-- Chat Messages Container with Blurry Effect -->
    <div class="h-[500px] overflow-y-auto p-6 space-y-4 backdrop-blur-sm bg-opacity-30 bg-dark">
      {#each messages as message}
        <div class="chat-message {message.role === 'user' ? 'flex justify-end' : ''}">
          <div class="{message.role === 'user' 
            ? 'bg-purple-800 bg-opacity-60 backdrop-blur-xs ml-12 rounded-lg p-4 max-w-[80%] shadow-lg' 
            : 'bg-purple-900 bg-opacity-50 backdrop-blur-xs mr-12 border-l-4 border-neon-purple rounded-lg p-4 max-w-[80%] shadow-lg'}">
            <p class="text-slate-100">{@html message.content.replace(/\n/g, '<br>')}</p>
          </div>
        </div>
      {/each}
  
      <!-- Thinking & Loading States -->
      {#if thinkingInfo}
        <div class="bg-purple-800 bg-opacity-40 backdrop-blur-xs border-l-4 border-neon-pink text-slate-200 p-4 rounded-md space-y-2 text-sm mr-12 shadow-lg">
          <p class="font-bold flex items-center"><span class="text-neon-pink mr-2">🔒</span> Anonymizing your message securely...</p>
          <div class="space-y-1 bg-purple-900 bg-opacity-60 p-3 rounded-md">
            <p><span class="font-semibold text-neon-blue">Original:</span> {thinkingInfo.original}</p>
            <p><span class="font-semibold text-neon-blue">Anonymized:</span> {thinkingInfo.anonymized}</p>
            <p><span class="font-semibold text-neon-blue">Report:</span> {thinkingInfo.report}</p>
          </div>
        </div>
      {:else if isLoading}
        <div class="flex items-center space-x-2 mr-12 bg-purple-800 bg-opacity-40 backdrop-blur-xs border-l-4 border-neon-blue rounded-lg p-4 shadow-lg">
          <div class="animate-pulse flex space-x-1">
            <div class="h-2 w-2 bg-neon-blue rounded-full"></div>
            <div class="h-2 w-2 bg-neon-blue rounded-full animation-delay-200"></div>
            <div class="h-2 w-2 bg-neon-blue rounded-full animation-delay-400"></div>
          </div>
          <span class="text-purple-200">Thinking...</span>
        </div>
      {/if}
  
      {#if error}
        <div class="bg-red-900 bg-opacity-40 backdrop-blur-xs border-l-4 border-red-500 text-white p-4 rounded-lg mr-12 shadow-lg">
          <p class="font-medium">{error}</p>
        </div>
      {/if}
    </div>
  
    <!-- Input Area -->
    <div class="p-4 bg-purple-950 bg-opacity-60 backdrop-blur-sm border-t border-purple-700">
      <div class="flex space-x-2">
        <textarea
          bind:value={query}
          on:keydown={handleKeydown}
          placeholder="Type your message here... (Press Enter to send)"
          rows="2"
          class="flex-1 px-4 py-3 bg-dark bg-opacity-80 text-purple-100 rounded-lg border border-purple-700 focus:ring-2 focus:ring-neon-purple focus:outline-none resize-none"
        ></textarea>
        <button
          on:click={sendQuery}
          class="px-6 py-2 bg-gradient-to-r from-neon-purple to-neon-blue hover:opacity-90 text-white font-medium rounded-lg shadow transition-all disabled:opacity-50 disabled:cursor-not-allowed flex items-center justify-center min-w-[80px]"
          disabled={isLoading || !query.trim()}
        >
          {#if isLoading}
            <div class="h-5 w-5 border-t-2 border-b-2 border-white rounded-full animate-spin"></div>
          {:else}
            Send
          {/if}
        </button>
      </div>
  
      <!-- Footer -->
      <footer class="mt-4 text-center text-xs text-purple-400">
        Using {DEFAULT_PROVIDER} • Model: {DEFAULT_MODEL} •
        <a
          href="http://localhost:8000/docs"
          class="text-neon-blue hover:text-neon-purple transition-colors"
          target="_blank"
          rel="noopener noreferrer"
        >API Docs</a>
      </footer>
    </div>
  </div>
  
  <style>
    .animation-delay-200 {
      animation-delay: 0.2s;
    }
    .animation-delay-400 {
      animation-delay: 0.4s;
    }
  </style>
  