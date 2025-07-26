<script>
  import { base } from '$app/paths';
  
  let mobileMenuOpen = false;
  
  const navItems = [
    { href: `${base}/`, label: 'Home' },
    { href: `${base}/rules`, label: 'Rules' },
    { href: `${base}/about`, label: 'About' },
    { href: `${base}/contact`, label: 'Contact' }
  ];
</script>

<header class="bg-white border-b border-gray-200">
  <div class="container">
    <div class="flex justify-between items-center h-16">
      <!-- Logo -->
      <div class="flex-shrink-0">
        <a href={`${base}/`} class="text-2xl font-bold text-gray-900 font-raleway">
          Rules Talk
        </a>
      </div>
      
      <!-- Desktop Navigation -->
      <nav class="hidden md:flex space-x-8">
        {#each navItems as item}
          <a 
            href={item.href}
            class="text-gray-700 hover:text-blue-600 px-3 py-2 text-sm font-medium transition-colors font-inter"
          >
            {item.label}
          </a>
        {/each}
      </nav>
    </div>
  </div>
  
  <!-- Mobile Navigation -->
  {#if mobileMenuOpen}
    <div class="md:hidden bg-white border-t border-gray-200">
      <div class="px-2 pt-2 pb-3 space-y-1">
        {#each navItems as item}
          <a 
            href={item.href}
            class="block px-3 py-2 text-base font-medium text-gray-700 hover:text-blue-600 hover:bg-gray-50 rounded-md transition-colors font-inter"
          >
            {item.label}
          </a>
        {/each}
      </div>
    </div>
  {/if}
</header> 