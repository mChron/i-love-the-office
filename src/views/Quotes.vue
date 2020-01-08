<template>
    <div class="quotes">
        <h1>That's What She Said</h1>
        <hr />
        <div class="d-flex justify-content-between align-items-end">
            <!-- Challenge 3 - Add drop-down filter here -->
            <div class="form-group">
                <label for="character-filter">Select Quotes By Character:</label>
                <!-- v-model is the 'watched' attribute -->
                <select class="form-control" id="character-filter" v-model="filterBy">
                    <option value="">All Quotes</option>
                    <option v-for="character in characters" :value="character.id">{{character.name}}</option>
                </select>
            </div>
            <!-- Challenge 7 - Add button to create new quote here -->
        </div>
        <div class="row row-cols-3 row-cols-md-2">
            <!-- Challenge 1 - Add quote snippet here -->
            <div v-for="quote in characterQuotes" :key="quote.id" class="col mb-4">
                <card :img-src="quote.character.image" :img-alt="'image of ' + quote.character.name" img-direction="left">
                    <div class="card-body">
                        <p class="card-text">{{quote.quote}}</p>
                        <p class="card-text text-right font-italic">
                            - {{quote.character.name}}
                        </p>
                        <p class="card-text text-right">
                            <!-- Challenge 2 - Add favorite toggle here -->
                            <button
                                class="btn btn-default btn-sm"
                                v-b-tooltip.hover
                                title="like"
                                style="font-size: 1.5rem;"
                                v-on:click="fav(quote.id)"
                            >
                                <span class="sr-only">like</span>
                                <i v-if="!quote.isFavorite" class="far fa-heart"></i>
                                <i v-else="quote.isFavorite" class="fas fa-heart text-danger"></i>
                            </button>
                        </p>
                    </div>
                </card>
            </div>
        <!-- Challenge 7 - Add modal to create new quote here -->
        </div>
    </div>
</template>

<script>
    import characters from '../data/characters';
    import quotes from '../data/quotes';
    import Card from '../components/Card';
    export default {
        name: "quotes",
        data() {
            return {
                quotes: quotes,
                characters: characters,
                filterBy: '',
                components: {
                    Card: Card
                }
            }
        },
        // you should avoid updating computed values
        computed: {
           characterQuotes() {
              let computedList = this.quotes.map(q => ({
                  ...q,
                  character: this.characters.find(c => c.id === q.characterId)
              }));
              if(this.filterBy) {
                  alert(this.filterBy)
                  return computedList.filter(quote => quote.character.id === this.filterBy)
              }
              else {
                  return computedList
              }
          }
        },
        methods: {
            fav: function(quoteId) {
                let quote = this.quotes.find(quote => quote.id === quoteId)
                quote.isFavorite = !quote.isFavorite
            }
        }
    };
</script>

<style lang="scss">
</style>
