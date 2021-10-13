<template>
    <div class="card">
        <div class="card-image">
            <figure>
                <img :src="isFront ? frontImage : backImage" :alt="pokeName+'image'">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
                <div class="media-content">
                    <p class="title is-4">#{{id}} {{pokeName}}</p>
                    <p class="subtitle is-6">
                        <span v-for="(type, index) in types" :key="index">{{type}} </span>
                    </p>
                </div>
            </div>
            <div class="content">
                <button @click="ChangeSprite">Change sprite</button>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from "axios";

    export default {
        props: {
            name: String,
            url: String,
        },
        created: function () {
            axios.get(this.url).then(res => {
                this.frontImage = res.data.sprites.front_default;
                this.backImage = res.data.sprites.back_default;
                this.id = res.data.id;
                res.data.types.forEach(item => {
                    this.types.push(item.type.name)
                    this.$emit("addType", {name: item.type.name, pokemonId: this.id})
                })
            })
        },
        data() {
            return {
                frontImage: "",
                backImage: "",
                types: [],
                id: "",
                isFront: true
            }
        },
        computed: {
            pokeName() {
                return this.name.charAt(0).toUpperCase() + this.name.slice(1);
            },
        },
        methods: {
            ChangeSprite() {
                this.isFront = !this.isFront;
            }
        }
    }
</script>

<style>
    .card {
        text-align: center;
        width: 256px;
        height: 256px;
        padding-top: 4%;
        margin: 1%;
    }

    .card:hover {
        background-color: rgba(160, 160, 160, 0.5);
    }
</style>