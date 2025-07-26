<script>
    export let acronym = "";
    export let fullName = "";
    export let backgroundImage = "";
    export let href = "";
</script>

<a {href} class="agency-card">
    <div 
        class="card-image" 
        style="background-image: url({backgroundImage});"
    ></div>
    <div class="card-content">
        <h3 class="card-title">{acronym}</h3>
        <p class="card-subtitle">{fullName}</p>
    </div>
</a>

<style>
    .agency-card {
        margin:0px;
        flex-direction: column;
        background-color: white;
        border-radius: 3px;
        box-shadow: 0 0px 4px rgba(0,0,0,0.1);
        overflow: hidden;
        width: 600px;
        height:450px;
        transition: transform 0.2s ease, box-shadow 0.2s ease;
        cursor: pointer;
        text-decoration: none;
        color: inherit;
    }

    .agency-card:hover {
        transform: translateY(-4px);
        box-shadow: 0 3px 8px rgba(0,0,0,0.15);
    }

    .card-image {
        height: 160px;
        background-size: cover;
        background-position: center;
        border-bottom: 1px solid #f0f0f0;
    }

    .card-content {
        padding: 8px;
        background: white;

    }

    .card-title {
        font-family: 'Raleway', sans-serif;
        font-size: 1.5rem;
        font-weight: 700;
        color: #333;
        margin: 0 0 4px 0;
    }

    .card-subtitle {
        font-family: 'Raleway', sans-serif;
        font-size: 0.9rem;
        color: #666;
        line-height: 1.2;
        margin: 0;
    }
</style>
