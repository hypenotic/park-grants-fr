<template v-if="this.$store.state.locationList != null">
    <section class="filter" >
        <div id="mobile-filter-trigger" v-on:click="filterTrigger" v-bind:class="{ 'not-hidden-mobile': this.$store.state.filterViewState }">
            <i class="fa fa-sliders" aria-hidden="true"></i> <span>Filtre</span>
        </div>
        <div class="filter-bar">
            <ul>
                <li>
                    <p>
                        <strong style="color: white;">Filtrer par</strong>: 
                        <span class="info" id="filter-dropdown" if v-on:click="filterTrigger">Type d'événement</span> 
                        <span id="copy-selected-acts">- (<span v-html="filterCount" style="font-weight: bold;"></span> sélectionné)</span>
                    </p>
                </li>
            </ul>

            <div class="activity-list" v-bind:class="{ 'not-hidden': this.$store.state.filterViewState }">
                <form>
                    <div class="activity-groups">
                        <div class="activity-groups__single mb30" v-for="parent in this.$store.state.activityList" :key="parent.id">
                            <div class="activity-groups__single__header">
                                <img :src="parent.icon" :alt="parent.name">
                                <h6 style="color: white;" v-html="parent.french[0]">
                                </h6>
                            </div>
                            <ul id="ck-button">
                                <li class="map-chbx-trigger" v-for="child in parent.children" :key="child.term_id"> 
                                    <label>
									<input type="checkbox" class="ck-box" @change="filterChange" hidden v-model="checkedCategories" :value="child.term_id" />
									<span>{{child.french[0]}}</span>
									</label>
                                </li>
                            </ul>
                        </div>
                    </div>
                    <div class="submit-bar">
                        <div class="submit-bar-wrapper">
                            <span id="whole-sentence-count"><span id="activities-selected" v-html="filterCount"></span> ACTIVITÉS SÉLECTIONNÉES. PRÊT?</span>
                            <div type="submit" class="button button--small" id="apply-search">Cherche!</div>
                            <div id="clear-filters" v-bind:class="[checkedCategories.length >0 ? '' : 'hidden-clear']"><span>EFFACER LE FILTRE D'ACTIVITÉS</span></div>
                        </div>
                    </div>
                </form>
            </div>
        </div>  

        <div class="legend">
            <ul>
                <li>Légende:</li>
                <li>                    
                    <app-marker color="green"></app-marker>
                    <span>- Passé</span>
                </li>
                <li>
                    <app-marker color="orange"></app-marker>
                    <span>- En moins de 30 jours</span>
                </li>
                <li>
                    <app-marker color="blue"></app-marker>
                    <span>- En plus de 30 jours</span>
                </li>    
            </ul>
        </div>      
        
        <ul class="map-type">
            <li id="map-view-trigger" v-on:click="listTrigger" class="view-trigger" v-bind:class="[this.$store.state.listViewState ? '' : 'active-trigger']"><i class="fa fa-map-o fa-2x" aria-hidden="true"></i></li>
            <li id="list-view-trigger" v-on:click="listTrigger" class="view-trigger" v-bind:class="[this.$store.state.listViewState ? 'active-trigger' : '']"><i class="fa fa-list fa-2x" aria-hidden="true"></i></li>
        </ul>
    </section>
</template>

<script>
    import Marker from './Marker.vue';
    export default {
        components: {
            appMarker: Marker
        },
        data() {
            return {
                showActivityList: false,
                filters: [],
                checkedCategories: [],
                clearFilterCheck: [],
                mobileFilter: false
            }
        },
        mounted() {
            let app = this;
            // Listen for when the filter submit button is pressed
            document.getElementById("clear-filters").onclick = function() {
                app.checkedCategories = [];
            };
        },
        methods: { 
            changeFilters() {
                console.log('change filters');

            },
            applyFilters() {
                console.log('apply filters');
            },
            filterChange() {
                // Check if there are any active category buttons
                if (this.checkedCategories.length > 0) {
                    this.$store.dispatch("filterChange", this.checkedCategories);
                    this.clearFilterCheck = [];
                } else {
                    // if not, just reset everything
                    this.$store.dispatch("clearFilters", 'active');
                    this.checkedCategories = [];
                    this.clearFilterCheck = ['all'];
                }
            },
            clearFilters(event) {
                // if (event.target.checked) {
                //     this.$store.dispatch("clearFilters", 'active');
                //     this.checkedCategories = [];
                // } else {
                //     return
                // }
            },
            listTrigger() {
                this.$store.dispatch("listViewState",this.$store.state.listViewState );

                // TK – Might wanna store the searchbox status in the store
                let input = document.getElementById('pac-input');
                if (input.classList.contains('small-search')) {
                } else {
                    input.classList.add('small-search');
                }
            },
            filterTrigger() {
                this.$store.dispatch("filterViewState",this.$store.state.filterViewState );
            }
        },
        computed: {
            filterCount() {
                return this.checkedCategories.length;
            }
        },
    }
</script>

<style lang="scss" scoped>

@import '../../styles/variables.scss';
@import '../../styles/components/filter.scss';

</style>