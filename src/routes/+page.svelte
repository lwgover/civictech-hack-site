<script>
  import { base } from '$app/paths';
  import Footer from '$lib/components/Footer.svelte';
  import AgencyCard from '$lib/components/Agency-Card.svelte';
  import homepageBackground from '../images/homepage-background.jpg';
  
  // Sample agency data
  const agencies = [
    {
      acronym: "CMS",
      fullName: "Centers for Medicare & Medicaid Services",
      backgroundImage: "/images/CMS.png",
      href: `${base}/docket`
    },
    {
      acronym: "FTA",
      fullName: "Federal Transit Administration",
      backgroundImage: "/images/FTA.png",
      href: `${base}/docket`
    },
    {
      acronym: "HUD",
      fullName: "Department of Housing and Urban Development",
      backgroundImage: "/images/HUD.png",
      href: `${base}/docket`
    }
  ];
  
  // Sample featured rules data
  const featuredRules = [
    {
      title: "Environmental Protection Standards",
      description: "New regulations for industrial emissions and waste management practices.",
      href: `${base}/rules/environmental-protection`
    },
    {
      title: "Consumer Data Privacy",
      description: "Enhanced protections for personal information in digital transactions.",
      href: `${base}/rules/consumer-privacy`
    },
    {
      title: "Healthcare Access Expansion",
      description: "Proposed changes to improve healthcare accessibility and affordability.",
      href: `${base}/rules/healthcare-access`
    },
    {
      title: "Small Business Support",
      description: "Regulatory relief measures for small and medium-sized businesses.",
      href: `${base}/rules/small-business`
    }
  ];
  
  const howItWorks = [
    {
      icon: 'document',
      title: 'Understand',
      description: 'Plain-language summaries of rules'
    },
    {
      icon: 'timeline',
      title: 'Track',
      description: 'Stay on top of comment deadlines'
    },
    {
      icon: 'comment',
      title: 'Comment',
      description: 'Submit your input directly'
    }
  ];
</script>

<svelte:head>
  <title>Talk to Me in Rules - Turning Public Comments into a Conversation</title>
  <meta name="description" content="Understand, track, and comment on public regulations with ease." />
</svelte:head>

<!-- Hero Section -->
<section class="relative min-h-screen flex items-center justify-center overflow-hidden">
  <!-- Background Image -->
  <div class="absolute inset-0 bg-cover bg-center bg-no-repeat" style="background-image: url({homepageBackground});"></div>
  
  <!-- Gradient Overlay -->
  <div class="absolute inset-0 bg-gradient-civic opacity-90"></div>
  
  <!-- Hero Content -->
  <div class="relative z-10 text-center px-4 lg:px-8 max-w-4xl mx-auto">
    <h1 class="text-5xl lg:text-7xl font-bold text-white font-raleway mb-6 leading-tight" style="font-weight:800; letter-spacing: 2px; padding-bottom:0px">
      <i>Talk to me in Rules</i>
    </h1>
    <p class="text-xl lg:text-2xl text-white opacity-90 font-inter mb-8 max-w-2xl mx-auto leading-relaxed" style="font-weight:200; padding-top:0px">
      Showing the conversations latent in Public Comments. 
    </p>
  </div>
</section>

<!-- Agency Cards Section -->
<section class="py-16 px-4 lg:px-8 bg-gray-50">
  <div class="max-w-7xl mx-auto">
    <h2 class="text-4xl font-bold text-center text-gray-800 mb-12 font-raleway">Explore Agencies</h2>
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
      {#each agencies as agency}
        <AgencyCard 
          acronym={agency.acronym}
          fullName={agency.fullName}
          backgroundImage={agency.backgroundImage}
          href={agency.href}
        />
      {/each}
    </div>
  </div>
</section>

<Footer />
