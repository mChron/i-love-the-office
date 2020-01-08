<template>
    <card :img-src="imgSrc" :img-alt="'image of ' + characterName" img-direction="left">
        <p class="card-text">{{quote}}</p>
        <p class="card-text text-right font-italic">
            - {{characterName}}
        </p>
        <p class="card-text text-right">
            <!-- Challenge 2 - Add favorite toggle here -->
            <button
                class="btn btn-default btn-sm"
                v-b-tooltip.hover
                title="like"
                style="font-size: 1.5rem;"
                v-on:click="toggleFavorite()"
            >
                <span class="sr-only">like</span>
                <i v-if="!favorite" class="far fa-heart"></i>
                <i v-else="favorite" class="fas fa-heart text-danger"></i>
            </button>
        </p>
    </card>
</template>

<script>
    import Card from './Card';

    export default {
        name: "Quote",
        components: {
            Card
        },
        methods: {
            toggleFavorite() {
                // have to emit an event up to the parent to properly modify the data
                this.$emit("favorite-clicked", this.quoteId);
            }
        },
        props: {
          imgSrc: {
              type: String,
              default:
                  "https://en.wikipedia.org/wiki/Dunder_Mifflin#/media/File:Dunder_Mifflin,_Inc.svg"
          },
          characterName: {
              type: String,
              default: "Unknown"
          },
          quote: {
              type: String,
              default:
                  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
          },
          quoteId: Number,
          favorite: Boolean
        }
    }
</script>

<style lang="scss">

</style>
