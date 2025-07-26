<script>
  import { onMount } from 'svelte';
  import Footer from '$lib/components/Footer.svelte';
  import Card from '$lib/components/Card.svelte';
  import homepageBackground from '../../images/homepage-background.jpg';
  
  let cmsData = null;
  let loading = true;
  let error = null;
  
  // Sentiment color mapping
  const sentimentColors = {
    positive: 'text-green-600 bg-green-100 p-1',
    negative: 'text-red-600 bg-red-100 p-1', 
    neutral: 'text-gray-600 bg-gray-100 p-1'
  };
  
  // Sentiment icon mapping
  const sentimentIcons = {
    positive: '👍',
    negative: '👎',
    neutral: '🤔'
  };
  
  onMount(async () => {
    try {
      // Only fetch data in the browser, not during prerendering
      if (typeof window !== 'undefined') {
        const response = await fetch('/example_data/CMS1.json');
        if (!response.ok) {
          throw new Error('Failed to load CMS data');
        }
        cmsData = await response.json();
      }
    } catch (err) {
      error = err.message;
    } finally {
      loading = false;
    }
  });
  
  // Group issues by sentiment for better organization
  $: issuesBySentiment = cmsData ? {
    positive: cmsData.issues.filter(issue => issue.sentiment === 'positive'),
    negative: cmsData.issues.filter(issue => issue.sentiment === 'negative'),
    neutral: cmsData.issues.filter(issue => issue.sentiment === 'neutral')
  } : {};
  
  // Get sentiment statistics
  $: sentimentStats = cmsData ? {
    total: cmsData.issues.length,
    positive: issuesBySentiment.positive?.length || 0,
    negative: issuesBySentiment.negative?.length || 0,
    neutral: issuesBySentiment.neutral?.length || 0
  } : {};
</script>

<svelte:head>
  <title>Docket - {cmsData?.policy_name || 'CMS Policy'} | Talk to Me in Rules</title>
  <meta name="description" content="Explore public comments and issues for the National Directory of Healthcare Providers & Services policy." />
</svelte:head>

<!-- Hero Section -->
<section class="relative min-h-screen flex items-center justify-center overflow-hidden">
  <!-- Background Image -->
  <div class="absolute inset-0 bg-cover bg-center bg-no-repeat" style="background-image: url({homepageBackground});"></div>
  
  <!-- Gradient Overlay -->
  <div class="absolute inset-0 bg-gradient-civic opacity-90"></div>
  
  <!-- Hero Content -->
  <div class="relative z-10 text-center px-4 lg:px-8 max-w-4xl mx-auto">
    <h1 class="text-5xl lg:text-7xl font-bold text-white font-raleway mb-6 leading-tight" style="font-weight:800; letter-spacing: 2px;">
      <i>Docket</i>
    </h1>
    {#if cmsData}
      <p class="text-xl lg:text-2xl text-white opacity-90 font-inter mb-8 max-w-3xl mx-auto leading-relaxed" style="font-weight:200;">
        {cmsData.policy_name}
      </p>
      <div class=" bg-opacity-20 rounded-xl p-6 text-white">
        <p class="text-lg font-inter mb-2">
          <span class="font-semibold">{cmsData.total_comments_processed}</span> comments processed
        </p>
        <p class="text-lg font-inter">
          <span class="font-semibold">{cmsData.issues.length}</span> key issues identified
        </p>
      </div>
    {:else if loading}
      <div class="bg-white bg-opacity-20 backdrop-blur-md rounded-xl p-6 text-white">
        <p class="text-lg font-inter">Loading docket data...</p>
      </div>
    {:else if error}
      <div class="bg-red-500 bg-opacity-20 backdrop-blur-md rounded-xl p-6 text-white">
        <p class="text-lg font-inter">Error loading docket data: {error}</p>
      </div>
    {/if}
  </div>
</section>

{#if cmsData}
  <!-- Sentiment Overview Section -->
  <section class="py-16 px-4 lg:px-8 bg-gray-50">
    <div class="max-w-7xl mx-auto">
      <h2 class="text-4xl font-bold text-center text-gray-800 mb-12 font-raleway">Public Sentiment Overview</h2>
      
      <!-- Sentiment Statistics -->
      <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-12">
        <div class="bg-white rounded-xl p-6 shadow-lg text-center">
          <div class="text-3xl font-bold text-gray-800 mb-2">{sentimentStats.total}</div>
          <div class="text-gray-600 font-inter">Total Issues</div>
        </div>
        <div class="bg-white rounded-xl p-6 shadow-lg text-center">
          <div class="text-3xl font-bold text-green-600 mb-2">{sentimentStats.positive}</div>
          <div class="text-gray-600 font-inter">Positive</div>
        </div>
        <div class="bg-white rounded-xl p-6 shadow-lg text-center">
          <div class="text-3xl font-bold text-red-600 mb-2">{sentimentStats.negative}</div>
          <div class="text-gray-600 font-inter">Negative</div>
        </div>
        <div class="bg-white rounded-xl p-6 shadow-lg text-center">
          <div class="text-3xl font-bold text-gray-600 mb-2">{sentimentStats.neutral}</div>
          <div class="text-gray-600 font-inter">Neutral</div>
        </div>
      </div>
    </div>
  </section>

  <!-- Issues by Sentiment -->
  <section class="py-16 px-4 lg:px-8 bg-white">
    <div class="max-w-7xl mx-auto">
      <!-- Negative Issues -->
      {#if issuesBySentiment.negative && issuesBySentiment.negative.length > 0}
        <div class="mb-16">
          <h3 class="text-3xl font-bold text-gray-800 mb-8 font-raleway flex items-center">
            <span class="mr-3">👎</span>
            Concerns & Opposition ({issuesBySentiment.negative.length})
          </h3>
          <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
            {#each issuesBySentiment.negative as issue}
              <Card title={issue.description} variant="elevated">
                <div class="space-y-4">
                  <div class="flex items-center justify-between">
                    <span class="text-sm font-semibold text-gray-500">Issue #{issue.issue_id}</span>
                    <span class="px-3 py-1 rounded-full text-sm font-semibold {sentimentColors.negative}">
                      {sentimentIcons.negative} Negative
                    </span>
                  </div>
                  
                  {#if issue.related_policy_sections && issue.related_policy_sections.length > 0}
                    <div>
                      <h4 class="text-sm font-semibold text-gray-700 mb-2">Related Policy Sections:</h4>
                      <div class="flex flex-wrap gap-2">
                        {#each issue.related_policy_sections as section}
                          <span class="px-2 py-1 bg-blue-100 text-blue-800 text-xs rounded-full">
                            {section}
                          </span>
                        {/each}
                      </div>
                    </div>
                  {/if}
                  
                  {#if issue.referencing_comments && issue.referencing_comments.length > 0}
                    <div>
                      <h4 class="text-sm font-semibold text-gray-700 mb-2">
                        Referenced in {issue.referencing_comments.length} comment{issue.referencing_comments.length !== 1 ? 's' : ''}:
                      </h4>
                      <div class="space-y-2">
                        {#each issue.referencing_comments.slice(0, 2) as comment}
                          <div class="bg-gray-50 rounded-lg p-3">
                            <p class="text-sm text-gray-600 italic">"{comment.excerpt}"</p>
                            <p class="text-xs text-gray-500 mt-2">Comment ID: {comment.comment_id}</p>
                          </div>
                        {/each}
                        {#if issue.referencing_comments.length > 2}
                          <p class="text-sm text-gray-500 italic">
                            +{issue.referencing_comments.length - 2} more comments...
                          </p>
                        {/if}
                      </div>
                    </div>
                  {/if}
                </div>
              </Card>
            {/each}
          </div>
        </div>
      {/if}

      <!-- Positive Issues -->
      {#if issuesBySentiment.positive && issuesBySentiment.positive.length > 0}
        <div class="mb-16">
          <h3 class="text-3xl font-bold text-gray-800 mb-8 font-raleway flex items-center">
            <span class="mr-3">👍</span>
            Support & Recommendations ({issuesBySentiment.positive.length})
          </h3>
          <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
            {#each issuesBySentiment.positive as issue}
              <Card title={issue.description} variant="elevated">
                <div class="space-y-4">
                  <div class="flex items-center justify-between">
                    <span class="text-sm font-semibold text-gray-500">Issue #{issue.issue_id}</span>
                    <span class="px-3 py-1 rounded-full text-sm font-semibold {sentimentColors.positive}">
                      {sentimentIcons.positive} Positive
                    </span>
                  </div>
                  
                  {#if issue.related_policy_sections && issue.related_policy_sections.length > 0}
                    <div>
                      <h4 class="text-sm font-semibold text-gray-700 mb-2">Related Policy Sections:</h4>
                      <div class="flex flex-wrap gap-2">
                        {#each issue.related_policy_sections as section}
                          <span class="px-2 py-1 bg-blue-100 text-blue-800 text-xs rounded-full">
                            {section}
                          </span>
                        {/each}
                      </div>
                    </div>
                  {/if}
                  
                  {#if issue.referencing_comments && issue.referencing_comments.length > 0}
                    <div>
                      <h4 class="text-sm font-semibold text-gray-700 mb-2">
                        Referenced in {issue.referencing_comments.length} comment{issue.referencing_comments.length !== 1 ? 's' : ''}:
                      </h4>
                      <div class="space-y-2">
                        {#each issue.referencing_comments.slice(0, 2) as comment}
                          <div class="bg-gray-50 rounded-lg p-3">
                            <p class="text-sm text-gray-600 italic">"{comment.excerpt}"</p>
                            <p class="text-xs text-gray-500 mt-2">Comment ID: {comment.comment_id}</p>
                          </div>
                        {/each}
                        {#if issue.referencing_comments.length > 2}
                          <p class="text-sm text-gray-500 italic">
                            +{issue.referencing_comments.length - 2} more comments...
                          </p>
                        {/if}
                      </div>
                    </div>
                  {/if}
                </div>
              </Card>
            {/each}
          </div>
        </div>
      {/if}

      <!-- Neutral Issues -->
      {#if issuesBySentiment.neutral && issuesBySentiment.neutral.length > 0}
        <div class="mb-16">
          <h3 class="text-3xl font-bold text-gray-800 mb-8 font-raleway flex items-center">
            <span class="mr-3">🤔</span>
            Questions & Clarifications ({issuesBySentiment.neutral.length})
          </h3>
          <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
            {#each issuesBySentiment.neutral as issue}
              <Card title={issue.description} variant="elevated">
                <div class="space-y-4">
                  <div class="flex items-center justify-between">
                    <span class="text-sm font-semibold text-gray-500">Issue #{issue.issue_id}</span>
                    <span class="px-3 py-1 rounded-full text-sm font-semibold {sentimentColors.neutral}">
                      {sentimentIcons.neutral} Neutral
                    </span>
                  </div>
                  
                  {#if issue.related_policy_sections && issue.related_policy_sections.length > 0}
                    <div>
                      <h4 class="text-sm font-semibold text-gray-700 mb-2">Related Policy Sections:</h4>
                      <div class="flex flex-wrap gap-2">
                        {#each issue.related_policy_sections as section}
                          <span class="px-2 py-1 bg-blue-100 text-blue-800 text-xs rounded-full">
                            {section}
                          </span>
                        {/each}
                      </div>
                    </div>
                  {/if}
                  
                  {#if issue.referencing_comments && issue.referencing_comments.length > 0}
                    <div>
                      <h4 class="text-sm font-semibold text-gray-700 mb-2">
                        Referenced in {issue.referencing_comments.length} comment{issue.referencing_comments.length !== 1 ? 's' : ''}:
                      </h4>
                      <div class="space-y-2">
                        {#each issue.referencing_comments.slice(0, 2) as comment}
                          <div class="bg-gray-50 rounded-lg p-3">
                            <p class="text-sm text-gray-600 italic">"{comment.excerpt}"</p>
                            <p class="text-xs text-gray-500 mt-2">Comment ID: {comment.comment_id}</p>
                          </div>
                        {/each}
                        {#if issue.referencing_comments.length > 2}
                          <p class="text-sm text-gray-500 italic">
                            +{issue.referencing_comments.length - 2} more comments...
                          </p>
                        {/if}
                      </div>
                    </div>
                  {/if}
                </div>
              </Card>
            {/each}
          </div>
        </div>
      {/if}
    </div>
  </section>
{/if}

<Footer /> 