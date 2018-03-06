<template>
    <div>  
        <footer v-if="this.$route.path == '/faq'">
            <div>
                <div class="columns">
                    <div class="column is-6">
                        <div class="columns is-centered">
                            <div class="column is-4">
                                <p>Sponsor fondateur</p>
                                <img src="https://parkpeople.ca/listings/custom/uploads/2017/09/TD-logo.png">
                            </div>
                        </div>
                    </div>
                    <div class="column is-6" style="background-color: green; color: white;">
                        <div class="columns">
                            <div class="column is-6">
                                <ul>
                                    <li style="color: white;font-weight: bold;">Park People</li>
                                    <li>401, rue Richmond Ouest</li>
                                    <li>Studio 119, laboratoire de City Builder</li>
                                    <li>Toronto, ON M5V 3A8</li>
                                </ul>
                                <ul class="details">
                                    <li>Téléphone: <a href="tel:+14165835776">416-583-5776</a></li>
                                    <li>Email: <a href="mailto:info@parkpeople.ca">info@parkpeople.ca</a></li>
                                    <li># Charité: 846449437RR0001</li>
                                </ul>
                                <ul class="social-links">
                                    <li><a href="https://parkpeople.ca/" target="_blank"><i class="fa fa-instagram" aria-hidden="true"></i></a></li>
                                    <li><a href="https://twitter.com/Park_People" target="_blank"><i class="fa fa-twitter" aria-hidden="true"></i></a></li>
                                    <li><a href="https://www.facebook.com/ParkPeopleTO/" target="_blank"><i class="fa fa-facebook" aria-hidden="true"></i></a></li>
                                </ul>
    
                            </div>
                            <div class="column is-6">
                                <a class="button" href="https://parkpeople.ca/donate-now" target="_blank">Faire un don</a>
                            </div>
    
                        </div>
                    </div>
                </div>
            </div>
        </footer> 
        <footer v-else class="footer-grants">
            <div>
                <div class="columns">
                    <div class="column is-6">
                        <div class="columns is-centered">
                            <div class="column is-4">
                                <p>Sponsor fondateur</p>
                                <img src="https://parkpeople.ca/listings/custom/uploads/2017/09/TD-logo.png">
                            </div>
                        </div>
                    </div>
                    <div class="column is-6" style="background-color: green; color: white;">
                        <div class="columns">
                            <div class="column is-6">
                                <ul>
                                    <li style="color: white;font-weight: bold;">Park People</li>
                                    <li>401, rue Richmond Ouest</li>
                                    <li>Studio 119, laboratoire de City Builder</li>
                                    <li>Toronto, ON M5V 3A8</li>
                                </ul>
                                <ul class="details">
                                    <li>Téléphone: <a href="tel:+14165835776">416-583-5776</a></li>
                                    <li>Email: <a href="mailto:info@parkpeople.ca">info@parkpeople.ca</a></li>
                                    <li># Charité: 846449437RR0001</li>
                                </ul>
                                <ul class="social-links">
                                    <li><a href="https://parkpeople.ca/" target="_blank"><i class="fa fa-instagram" aria-hidden="true"></i></a></li>
                                    <li><a href="https://twitter.com/Park_People" target="_blank"><i class="fa fa-twitter" aria-hidden="true"></i></a></li>
                                    <li><a href="https://www.facebook.com/ParkPeopleTO/" target="_blank"><i class="fa fa-facebook" aria-hidden="true"></i></a></li>
                                </ul>
    
                            </div>
                            <div class="column is-6">
                                <a class="button" href="https://parkpeople.ca/donate-now" target="_blank">Faire un don</a>
                            </div>
    
                        </div>
                    </div>
                </div>
            </div>
        </footer> 
    </div>
</template>

<script>
    import NewsletterForm from './NewsletterForm.vue';
    export default {
        components: {
            appForm: NewsletterForm
        }
    }
</script>

<style lang="scss" scoped>

    // Import Variables
    @import '../styles/variables.scss';

    .button {
        color: $white;
        background-color: $blue;
        font-family: $family-sanserif;
        font-weight: bold;
        border: 2px solid $blue;
        border-radius: 50px;
        padding: 8px 24px;
        &:hover {
            border: 2px solid $blue;
            background-color: $white;
            color: $blue; 
        }
    }

    footer {
        font-size: 0.8rem;
        p, ul, li {
            font-size: 0.8rem;
        }
        ul + ul {
            margin-top: 16px;
        }
    }

    footer {
        position: relative;
        padding-top: 200px;
        > div {
            position: relative;
            &:before {
                content: '';
                position: absolute;
                left: 0;
                top: -70px;
                width: 100%;
                height: 160px;
                background: #fff;
                -webkit-transform: skewY(5deg);
                -moz-transform: skewY(5deg);
                -ms-transform: skewY(5deg);
                -o-transform: skewY(5deg);
                transform: skewY(5deg);
                -webkit-backface-visibility: hidden;
            }
        }
    }

    footer.footer-grants {
        position: relative;
        padding-top: 150px;
        > div {
            position: relative;
            &:before {
                content: '';
                position: absolute;
                left: 0;
                top: -70px;
                width: 100%;
                height: 160px;
                background: $white;
                // -webkit-transform: skewY(5deg);
                // -moz-transform: skewY(5deg);
                // -ms-transform: skewY(5deg);
                // -o-transform: skewY(5deg);
                // transform: skewY(5deg);
                // -webkit-backface-visibility: hidden;
                @media #{$large-and-up} {
                    -webkit-transform: skewY(5deg);
                    -moz-transform: skewY(5deg);
                    -ms-transform: skewY(5deg);
                    -o-transform: skewY(5deg);
                    transform: skewY(5deg);
                }
                @media #{$xlarge-and-up} {
                    -webkit-transform: skewY(3deg);
                    -moz-transform: skewY(3deg);
                    -ms-transform: skewY(3deg);
                    -o-transform: skewY(3deg);
                    transform: skewY(3deg);
                }
            }
        }
    }

    footer >div >div >div {
        padding-top: 200px;
    }
    footer >div >div >div:first-child {
        background: rgb(249, 249, 249);
        @media #{$small-and-down} {
			text-align: center;
		}
    }
    footer >div >div >div:last-child {
        padding: 200px 80px 80px;
        @media #{$small-and-down} {
			padding: 80px;
		}
    }

    footer img {
        max-width: 150px;
        height: auto;
        padding-top: 0px;
    }

    .social-links {
        li {
            display: inline-block;
            a {
                color: white;
                &:hover {
                    opacity: 0.6;
                }
            }
            i {
                font-size: 32px;
            }
        }
        li + li {
            margin-left: 16px;
        }
    }
    .details a {
        color: white;
        text-decoration: underline;
        &:hover {
            text-decoration: none;
        }
    }
</style>