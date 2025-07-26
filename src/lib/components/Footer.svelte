<script>
    import { base } from '$app/paths';
    
    const footerLinks = [
        { href: `${base}/about`, label: "About" },
        { href: `${base}/contact`, label: "Contact" },
        { href: `${base}/data`, label: "Open Data" },
        { href: `${base}/privacy`, label: "Privacy" },
    ];
</script>

<footer class="bg-gradient-gray text-white">
    <!-- Bottom Section -->
    <div
        class="border-t border-gray-700 mt-8 pt-8 flex flex-col md:flex-row justify-between items-center"
    >
        <p class="text-gray-400 font-inter text-sm">
            © 2025 Rules Talk. All rights reserved.
        </p>
  </div>
</footer>
