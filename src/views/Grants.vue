<template>
	<div v-if="data != null">

		<section class="videos">
			<div class="overlay">
				<h1>
					Faites de vos parcs des lieux exceptionnels.
				</h1>
				<router-link v-if="data.meta_box._page_grant_cta_text" class="cta_button" :to="data.meta_box._page_grant_cta_link" v-html="data.meta_box._page_grant_cta_text"></router-link>
			</div>
			<div class="hero" v-if="isMobile()">
				<iframe v-if="selectedVideo == 0" src="https://player.vimeo.com/video/374742599?background=1&loop=1&autoplay=0" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
				<iframe v-if="selectedVideo == 1" src="https://player.vimeo.com/video/374961083?background=1&loop=1&autoplay=0" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
				<iframe v-if="selectedVideo == 2" src="https://player.vimeo.com/video/374963755?background=1&loop=1&autoplay=0" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
			</div>
			<div class="hero" v-else>
				<iframe v-if="selectedVideo == 0" src="https://player.vimeo.com/video/374742599?background=1&loop=1" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
				<iframe v-if="selectedVideo == 1" src="https://player.vimeo.com/video/374961083?background=1&loop=1" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
				<iframe v-if="selectedVideo == 2" src="https://player.vimeo.com/video/374963755?background=1&loop=1" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
			</div>
		</section>

		<section class="section" v-if="data && data.hasOwnProperty('meta_box')">
			<div class="container">
				<h1 id="bird-anchor" v-html="data.meta_box._page_grant_heading"></h1>
				<div class="topContent" v-html="data.content.rendered"></div>
			</div>
		</section>
		<section class="map-section">
			<h2>Activités TD Park People au Canada</h2>
			<app-map></app-map>
		</section>
				
		<section v-if="data.meta_box._page_grant_cta_text" class="recipients">
			<div class="align-center">
				<router-link class="cta_button" :to="data.meta_box._page_grant_cta_link" v-html="data.meta_box._page_grant_cta_text"></router-link>
			</div>
		</section>

		<section class="event-templates">
			<h3 v-html="data.meta_box._page_buckets_main_heading"></h3>
			<div class="four-column wow fadeInUp">
				<div v-for="bucket in data.meta_box._page_buckets" :key="bucket.bucket_copy">
					<h4 v-html="bucket._page_bucket_heading"></h4>
					<p v-html="bucket._page_bucket_copy"></p>
					<a :href="bucket._page_bucket_link" @click="downloadArea(bucket._page_bucket_heading)">Télécharger fichier .zip</a>
				</div>
			</div>
		</section>

		<section class="grant-illustration">
			<img src="https://parkpeople.ca/custom/uploads/2020/04/TD_PPgrants_isolation_webart.jpg" alt="Illustration">
			<!-- <div class="main-animation">
			</div> -->
			<!-- <div class="clouds">
			</div> -->
		</section>

		<section class="grants-newsletter">
			<div class="container">
				<!-- <p>Want to stay up-to-date on Park People news?</p> -->
				<a class="button" href="http://eepurl.com/dx3BWX" target="_blank">Recevez notre newsletter!</a>
			</div>
		</section>
		<section class="grant-sponsors">
			<p>Rendu possible grâce à une formidable collaboration:</p>
			<ul>
				<li v-for="sponsor in data.meta_box._page_grant_sponsors" :key="sponsor['_page_g_sponsor_img']">
					<a :href="sponsor['_page_g_sponsor_link']" target="_blank"><img :src="sponsor['_page_g_sponsor_img']" alt="logo"></a>
				</li>
			</ul>
		</section>
		<!-- <section class="related-resources" id="related-resources-jump">
			<h3 v-html="data.meta_box._page_grant_resource_heading"></h3>
			<div class="related-resources-copy" v-html="data.meta_box._page_grant_resource_copy"></div>
			<div class="wide-container">
				<div class="columns is-multiline">
					<div class="column is-one-quarter" v-for="related in relatedPosts" :key="related.title.rendered">
						<div class="card">
							<div class="card-image">
								<figure class="image is-2by1">
									<img v-if="related._embedded['wp:featuredmedia'] != undefined" :src="related._embedded['wp:featuredmedia'][0].media_details.sizes.medium.source_url">
								</figure>
							</div>
							<div class="card-content">
								<div class="content">
									<small style="font-family: 'Dosis';font-size: 12px;"> {{ related.type | removeHyphen | toTitleCase }}</small>

									<a :href="'https://parkpeople.ca/resources/en/'+related.type + '/' + related.id + '/' + related.slug"><h4 v-html="related.title.rendered"></h4></a>
									<div v-html="$options.filters.readMore(related.excerpt.rendered, 100, '...')"></div>
									<div v-if="related.pure_taxonomies.activity" class="activity-list-container">
										<strong>Do in parks</strong>: <span v-for="tax in related.pure_taxonomies.activity" :key="tax.name">{{ tax.name  }}</span>
									</div>
									<div v-if="related.pure_taxonomies.learn" class="activity-list-container">
										<strong>Know about parks:</strong> <span v-for="tax in related.pure_taxonomies.learn" :key="tax.name">{{ tax.name }}</span>
									</div>
									
								</div>
							</div>
						</div>
					</div>
				</div>
			</div>
		</section> -->
		<app-related :title="data.meta_box._page_grant_resource_heading" :copy="data.meta_box._page_grant_resource_copy" :posts="relatedPosts"></app-related>
	</div>
	<div v-else class="loading-panel">
		<div>
			<img src="https://parkpeople.ca/custom/uploads/2018/01/birdflying_pp_small.gif" alt="">
		</div>
	</div>
</template>


<script>
import axios from 'axios';
import Map from '../components/map/Map.vue';
import RelatedList from '../components/related-resources/RelatedList.vue';
import { mapState } from 'vuex'
// import NewsletterForm from '../components/NewsletterForm.vue';
export default {
	components: {
        appMap: Map,
		appRelated: RelatedList
    },
	data() {
		return {
			data: null,
			relatedPosts: [],
			errors: [],
			loading: true,
			selectedVideo: 0,
			// videoLengths: [5,5,5],
			videoLengths: [72,61,65],
			time: 0
		};
	},
	filters: {
		translatedType(type){
			if (type == 'resource') {
				return 'ressource'
			} else if ( type == 'research') {
				return 'recherche'
			} else {
				return 'étude de cas'
			}
		},
		removeHyphen(value){
			return value.replace("-", ' ');
		},
		capitalizeFirstLetter(value) {
			return value.charAt(0).toUpperCase() + value.slice(1);
		},
		toUppercase(value) {
			return value.toUpperCase();
		},
		readMore(value, length, suffix) {
			if (value.length < length)
			return value;	
			return value.substring(0, length) + suffix;
		},
		stripHTML(value) {
			return value.replace(/(<([^>]+)>)/ig,"");
		},
		toTitleCase(value) {
    		return value.replace(/\w\S*/g, (txt) => {
				return txt.charAt(0).toUpperCase() + txt.substr(1).toLowerCase();
			});
		},
	},
	computed: {

    },
	methods: {
		downloadArea(name) {
			console.log('download event', name);
			this.$ga.event('download', 'Bourses TD PP', name, 1);
		},
		isMobile() {
			return (navigator.userAgent.match(/Android/i)
			|| navigator.userAgent.match(/webOS/i)
			|| navigator.userAgent.match(/iPhone/i)
			|| navigator.userAgent.match(/iPad/i)
			|| navigator.userAgent.match(/iPod/i)
			|| navigator.userAgent.match(/BlackBerry/i)
			|| navigator.userAgent.match(/Windows Phone/i))
		}
	},
	mounted(){
		this.selectedVideo = Math.floor(Math.random()*3);
		var ctx = this;
		setInterval(function(){
			ctx.time += 1;
			ctx.time < 10 ? console.log(ctx.time) : "";
			if(ctx.time == ctx.videoLengths[ctx.selectedVideo]){
				console.log(ctx.selectedVideo);
				ctx.selectedVideo = (ctx.selectedVideo + 1) % 3;
			}
		}, 1000);
	},
	created() {
		// console.log(store.state.count)
		axios.get('https://parkpeople.ca/wp-json/wp/v2/pages/17551?_embed')
		.then(response => {
            console.log(response.data)
			this.data = response.data
			axios.all([
				axios.get('https://parkpeople.ca/wp-json/wp/v2/case-study/?_embed&categories=134&per_page=15&lang=fr'),
				axios.get('https://parkpeople.ca/wp-json/wp/v2/research/?_embed&categories=134&per_page=15&lang=fr'),
				axios.get('https://parkpeople.ca/wp-json/wp/v2/resource/?_embed&categories=134&per_page=15&lang=fr')
			])
			.then(axios.spread((response, response1, response2) => {
				// console.log(response.data)
				let allPosts  = response.data.concat(response1.data, response2.data);
				console.log('old', allPosts)
				allPosts.sort(function(a,b){
					return new Date(b.date) - new Date(a.date)
				})	
				console.log('sorted', allPosts)
				this.relatedPosts = allPosts
			}))
			.catch(e => {
				this.errors.push(e)
			})
		})
		.catch(e => {
			this.errors.push(e)
		})
	},
};
</script>

<style lang="scss" scoped>

@import '../styles/variables.scss';
@import '../styles/views/home.scss';

</style>