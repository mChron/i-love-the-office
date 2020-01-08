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
                <quote :img-src="quote.character.image"
                    :character-name="quote.character.name"
                    :favorite="quote.isFavorite"
                    :quote-id="quote.id"
                    :quote="quote.quote"
                    @favorite-clicked="fav">
                </quote>
            </div>
            <div>
              <quote></quote>
            </div>
        <!-- Challenge 7 - Add modal to create new quote here -->
        </div>
    </div>
</template>

<script>
    import characters from '../data/characters';
    import quotes from '../data/quotes';
    import Card from '../components/Card';
    import Quote from '../components/Quote';
    export default {
        name: "quotes",
        data() {
            return {
                quotes: quotes,
                characters: characters,
                filterBy: ''
            }
        },
        components: {
            Card: Card,
            Quote: Quote
        },
        // you should avoid updating computed values
        computed: {
           characterQuotes() {
              let computedList = this.quotes.map(q => ({
                  ...q,
                  character: this.characters.find(c => c.id === q.characterId)
              }));
              if(this.filterBy) {
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
