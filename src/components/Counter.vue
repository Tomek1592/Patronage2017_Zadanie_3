<template>
    <div class="score">
        <div class="columns">
            <div class="column is-10 hr-title">
                <i class="counter-title">Score {{ currentId }}</i>
            </div>
            <hr>
            <div class="column is-2">
                <button class="btn btn-close"
                        @click="remove">X</button>
            </div>
        </div>
        <div class="columns">
                <span class="counter-value animated fadeInDownBig">{{ counterValue }}</span>
        </div>
        <div class="columns">
            <div class="control is-grouped btn-wrapper">
                <a class="button btn-counter btn-up"
                   :class="{ 'btn-counter-disabled': isMax }"
                   @click="up"
                   :disabled="isMax">+</a>
                <a class="button btn-counter btn-down"
                   :class="{ 'btn-counter-disabled': isZero }"
                   @click="down"
                   :disabled="isZero">-</a>
            </div>
        </div>
        <div class="columns">
            <div class="column">
                <input class="input is-large"
                       type="number"
                       v-model="currentNewValue"
                       :placeholder="placeholderMessage"
                       :class="{ 'is-error animated shake': hasError }">
            </div>

        </div>
        <div class="control is-grouped">
            <a class="button btn-api btn-get"
               @click="getValue">Get</a>
            <a class="button btn-api btn-set"
               :counterNewValue="counterNewValue"
               @click="setValue">Set</a>
            <a class="button btn-api btn-reset"
               :disabled="isZero"
               @click="resetValue"
               :class="{ 'btn-disabled': isZero }">Reset</a>
        </div>

        <modal v-if="showModal"
               :showModal="showModal"
               :currentId="currentId"
               @close="showModal = false"
               :currentValue="currentValue"></modal>
    </div>
</template>

<script>
    import GetModal from './GetModal.vue'
    export default {
        name: "Counter",
        data () {
            return {
                currentId: this.id,
                currentValue: this.value,
                currentFormat: this.format,
                currentNewValue: '',
                placeholder: '',
                hasError: false,
                isZero: false,
                isMax: false,
                showModal: false
            }
        },

        props: ["value", "format", "id"],

        computed: {
            counterValue () {
                let stringValue = this.currentValue + ''

                while (stringValue.length < this.currentFormat) {
                    stringValue = '0' + stringValue
                }

                this.currentValue = stringValue

                if (Number(this.currentValue) === 0) {
                    this.isZero = true
                } else {
                    this.isZero = false
                }

                if (Number(this.currentValue) === Math.pow(10, this.currentFormat) - 1) {
                    this.isMax = true
                } else {
                    this.isMax = false
                }

                return this.currentValue
            },

            placeholderMessage () {
                if (!this.hasError) {
                    return this.placeholder = 'Type a number here.'
                } else {
                    if (Number(this.currentValue) === this.currentNewValue) {
                        let errorMessage = 'You entered the same number!'
                        this.currentNewValue = ""
                        return this.placeholder = errorMessage
                    } else {
                        let number = Math.pow(10, this.currentFormat) - 1
                        let errorMessage = 'Type number from 0 to ' + number
                        this.currentNewValue = ""
                        return this.placeholder = errorMessage
                    }
                }
            },

            counterNewValue () {
                let isBelowZero = this.currentNewValue < 0
                let isAboveMax =
                    this.currentNewValue > Math.pow(10, this.currentFormat) - 1

                if (isBelowZero || isAboveMax) {
                    this.hasError = true
                    this.currentNewValue = ''
                } else {
                    this.hasError = false
                }
            },
        },

        methods: {
            up (event) {
                event.preventDefault()

                this.hasError = false
                if (this.currentValue < Math.pow(10, this.currentFormat) - 1) {
                    this.currentValue++
                }
            },

            down (event) {
                event.preventDefault()

                this.hasError = false
                if (this.currentValue > 0) {
                    this.currentValue--
                }
            },

            setValue (event) {
                event.preventDefault()

                if (this.currentNewValue !== "") {
                    this.currentValue = Number.parseInt(this.currentNewValue)
                    this.currentNewValue = ""
                } else {
                    this.hasError = true
                    this.currentNewValue = ""
                }
            },

            getValue (event) {
                event.preventDefault()
                this.showModal = true
            },

            resetValue (event) {
                event.preventDefault()

                if (this.currentValue > 0) {
                    this.currentValue = 0
                    this.hasError = false
                } else {
                    this.hasError = false
                }
            },

            remove () {
                this.$emit("remove", this.currentId);
            }
        },

        components: {
            "modal": GetModal
        }
    }
</script>

<style>
    @import url("https://fonts.googleapis.com/css?family=Orbitron:400,900");

    ::-webkit-input-placeholder { /* Chrome/Opera/Safari */
        color: #a0a0a0;
        text-align: center;
        font-family: 'Orbitron', sans-serif;
        font-size: 18px;
    }
    input.is-error::-webkit-input-placeholder { /* Chrome/Opera/Safari - when error occurs*/
        color: red;
        text-align: center;
        font-family: 'Orbitron', sans-serif;
        font-size: 18px;
    }
    ::-moz-placeholder { /* Firefox 19+ */
        color: #a0a0a0;
        text-align: center;
        font-family: 'Orbitron', sans-serif;
        font-size: 18px;
    }
    :-ms-input-placeholder { /* IE 10+ */
        color: #a0a0a0;
        text-align: center;
        font-family: 'Orbitron', sans-serif;
        font-size: 18px;
    }
    :-moz-placeholder { /* Firefox 18- */
        color: #a0a0a0;
        text-align: center;
        font-family: 'Orbitron', sans-serif;
        font-size: 18px;
    }

    input:focus {
        border: none;
    }

    html {
        background-color: #f5da55;
    }

    .score {
        height: 390px;
        width: 400px;
        background-color: #323330;
        margin: 90px 50px -32px 50px;
        padding: 20px;
        display: inline-block;
        border-radius: 4px;
        box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
    }

    .counter-title {
        color: #F5DA55;
        font-size: 30px;
        float: left;
    }

    .hr-title {
        border-bottom: 3px dotted #F5DA55;
        margin-left: 15px;
    }

    .counter-value {
        color: #f5da55;
        font-size: 70px;
        vertical-align: top;
        margin: 0 auto;
    }

    .btn {
        border: none;
        border-radius: 3px;
    }

    .btn:focus {
        outline: 0;
    }

    .btn-wrapper {
        margin: 0 auto;
    }

    .btn-counter {
        width: 50px;
        height: 50px;
        padding: 5px;
        margin: 0 3px 15px 3px;
        border: none;
        border-radius: 3px;
        color: white;
        font-size: 40px;
    }

    .btn-counter:hover {
        position: relative;
        top: 2px;
    }

    .btn-up {
        background-color: #1abc9c;
        float: right;
    }

    .btn-down {
        background-color: #f6223f;
        float: left;
    }

    .btn-api {
        height: 40px;
        width: 120px;
        background-color: #323330;
        border: 1px dotted #f5da55;
        font-family: 'Orbitron', sans-serif;
        font-size: 18px;
        color: white;
    }

    .btn-api:hover {
        background-color: #f5da55;
        color: #323330;
    }

    .btn-close {
        color: #F5DA55;
        background: none;
        margin-right: 20px;
        margin-top: 4px;
        font-size: 20px;
    }

    .btn-close:hover {
        font-size: 25px;
        color: white;
    }

    .btn-disabled,
    .btn-counter-disabled {
        background-color: #6d6d6d !important;
    }

    .btn-disabled:hover {
        color: white;
        border: 1px dotted #f5da55;
    }

    .btn-counter-disabled:hover {
        color: white;
        position: relative;
        top: 0;
    }

    .is-error {
        border: 2px solid red;
    }

    @keyframes fadeInDownBig {
        from {
            opacity: 0;
            transform: translate3d(0, -25px, 0);
        }

        to {
            opacity: 1;
            transform: none;
        }
    }

    .fadeInDownBig {
        animation-name: fadeInDownBig;
    }
</style>

















