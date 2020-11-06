<script>
	export let items;
	export let testimonials;
</script>
<script context="module">
	import PrismicHTML from '../components/PrismicHTML.svelte';
	import Prismic from 'prismic-javascript';
	import PrismicDOM from 'prismic-dom';
	import { Client } from '../../prismic-config.js';

	let items;
	let testimonials;

	export async function preload({ params, query }) {
		const contentResponse = await Client.query(
				Prismic.Predicates.at('document.type', 'content'),
                { orderings : '[my.content.date]' }
		)

		const testimonialResponse = await Client.query(
				Prismic.Predicates.at('document.type', 'testimonial')
		)


		items = contentResponse.results
		testimonials = testimonialResponse.results


		if (items && testimonials) {
			return {items,testimonials};
        } else {
          this.error(res.status, data.message);
        }
	}

</script>

<svelte:head>
<title>Angel People Solutions Ltd.</title>
</svelte:head>

<div class="uk-container uk-margin-large-top">


<div class="uk-grid-column-small uk-grid-row-large" uk-grid>
{#each items as item}
<div class="uk-width-1-4@m uk-margin-large-top" uk-scrollspy="cls: uk-animation-slide-left; repeat: true">
<h2>{PrismicDOM.RichText.asText(item.data.title)}</h2>
</div>
<div class="uk-width-3-4@m uk-margin-large-top" uk-scrollspy="cls: uk-animation-slide-right; repeat: true">
<PrismicHTML elements={item.data.content} />
</div>
{/each}

<div class="uk-width-1-4@m uk-margin-large-top" uk-scrollspy="cls: uk-animation-slide-left; repeat: true">
<h2>Contact</h2>
</div>
<div class="uk-width-3-4@m uk-margin-large-top" uk-scrollspy="cls: uk-animation-slide-right; repeat: true">
<ul class="uk-list">
<li>Angel People Solutions Ltd</li>
<li>87 Old Wokingham Road</li>
<li>Crowthorne</li>
<li>Berkshire</li>
<li>RG45 6LJ</li>
<li>Tel: <a href="tel:+447876648146">07876 648146</a></li>
<li>Email: <a href="mailto:jacqui@angelps.co.uk">jacqui@angelps.co.uk</a></li>
<li><a href="https://uk.linkedin.com/in/jacqui-angel-48276b11" ><span uk-icon="icon: linkedin"></span></a></li>
</ul>
</div>

</div>

</div>

<div class="uk-section testimonials">
<div class="uk-container">
<div class="uk-width-1-1@m" >
<h3>Our Clients</h3>
<div  class="uk-slideshow" uk-slideshow="autoplay: true; animation: slide">
<ul class="uk-slideshow-items">
{#each testimonials as testimonial}
<li>
<h4>{PrismicDOM.RichText.asText(testimonial.data.title)}</h4>
<PrismicHTML elements={testimonial.data.content} />
</li>
{/each}
</ul>
</div>
</div>
</div>
</div>




<style>

	h2 {
		padding: 0;
		margin: 0;
        font-family: lato, sans-serif;
        font-size: 2.5rem !important;
		font-weight: 600;
        color: #004e92;
	}

   h3 {
        font-family: lato, sans-serif;
        font-size: 2rem !important;
        font-weight: 500 !important;
        margin-bottom: 3rem !important;
        color: white;
    }

    .testimonials {
    margin-top: 6rem;
    background-color: #004e92;
        font-family: lato, sans-serif;
    font-weight: 400 !important;
    font-size: 1.25rem !important;
    line-height: 1.5 !important;
    color: white !important;
    }



    .uk-list li {
     padding: 0;
     margin: 0;
        font-family: lato, sans-serif;
     font-weight: 400 !important;
     font-size: 1.25rem !important;
     line-height: 1.5;
     color: #004e92 !important;
    }

    .uk-list li a span{
        padding: 0.125rem !important;
        border-radius: 0.25rem !important;
        background: #004e92 !important;
        color: #FFFFFF !important;
    }

.uk-slideshow {
  color: #FFFFFF !important;
}

.uk-slideshow-items {
 color: #FFFFFF !important;
    min-height: 20rem !important;
}


    @media (max-width: 414px) {
        .uk-slideshow-items {
            min-height: 40rem !important;
        }

    }

    @media (max-width: 375px) {
        .uk-slideshow-items {
            min-height: 40rem !important;
        }
    }

    @media (max-width: 320px) {
        .uk-slideshow-items {
                min-height: 40rem !important;
        }
    }


</style>


