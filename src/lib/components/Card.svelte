<script>
  export let title = '';
  export let description = '';
  export let href = null;
  export let variant = 'default';
  
  const variants = {
    default: 'bg-white shadow-lg hover:shadow-xl',
    elevated: 'bg-white shadow-xl hover:shadow-2xl',
    outline: 'bg-transparent border-2 border-gray-200 hover:border-gray-300'
  };
</script>

<div class="group {variants[variant]} rounded-xl p-6 transition-all duration-300 hover:-translate-y-1">
  {#if title}
    <h3 class="text-xl font-bold text-gray-900 mb-3 font-raleway">
      {#if href}
        <a href={href} class="hover:text-blue-600 transition-colors">
          {title}
        </a>
      {:else}
        {title}
      {/if}
    </h3>
  {/if}
  
  {#if description}
    <p class="text-gray-600 mb-4 font-inter leading-relaxed">
      {description}
    </p>
  {/if}
  
  <slot />
  
  {#if href}
    <div class="mt-4">
      <a 
        href={href}
        class="inline-flex items-center text-blue-600 hover:text-blue-700 font-semibold transition-colors group-hover:translate-x-1"
      >
        View Details
        <svg class="w-4 h-4 ml-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path>
        </svg>
      </a>
    </div>
  {/if}
</div> 