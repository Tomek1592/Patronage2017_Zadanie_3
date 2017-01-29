<template>
    <div id="app">
        <div class="columns">
            <div class="column button-section">
                <button class="add-counter"
                        @click="showModal = true">+</button>
            </div>
        </div>

        <div class="counters-wrapper">
            <counter v-for="item in counters"
                     :id="item.id"
                     :key="item.id"
                     :value="item.value"
                     :format="item.format"
                     @remove="remove"></counter>
        </div>

        <newCounterModal v-on:newCounter="addCounter"
                         v-if="showModal"
                         :showModal="showModal"
                         @close="showModal = false"></newCounterModal>

    </div>
</template>

<script>
    import Counter from './components/Counter.vue'
    import NewCounterModal from './components/NewCounterModal.vue'
    export default {
        name: 'app',
        data () {
            return {
                showModal: false,
                hasError: false,
                newId: 1,
                lastElement: [],
                counters: [
                    {
                        id: 1,
                        value: 1,
                        format: 2
                    },
                    {
                        id: 2,
                        value: 101,
                        format: 4
                    }
                ],
            }
        },

        methods: {
            addCounter (newCounterValue, newCounterFormat) {
                if (this.counters.length !== 0) {
                    this.lastElement = this.counters[this.counters.length - 1]
                    this.newId = this.lastElement.id + 1
                } else {
                    this.newId = 1
                }

                let newCounter = {
                    value: newCounterValue,
                    format: newCounterFormat,
                    id: this.newId,
                }

                this.counters.push(newCounter)
                this.showModal = false
            },

            remove (id) {
                this.counters = this.counters.filter(function(el) {
                   if (el.id !== id) {
                       return el.id
                   }
                })
            }
        },

        components: {
            "counter": Counter,
            "newCounterModal": NewCounterModal
        }
    }
</script>

<style>
    #app {
        font-family: Orbitron;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }

    .add-counter {
        width: 100px;
        height: 100px;
        border: none;
        border-radius: 5px;
        background-color: #323330;
        box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
        color: #f5da55;
        font: normal normal normal 85px/1 FontAwesome;
    }

    .button-section {
        height: 100px;
    }

    .add-counter:focus {
        outline: 0;
    }

    .add-counter:hover {
        width: 120px;
        height: 120px;
        color: whitesmoke;
    }
</style>
