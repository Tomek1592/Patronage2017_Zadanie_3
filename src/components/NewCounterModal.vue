<template>
    <div class="modal" :class="{ 'is-active': showModal }">
        <div class="modal-background" @click="$emit('close')"></div>
        <div class="modal-content animated slideInDown">
            <div class="box">
                <div class="columns">
                    <div class="column is-8 is-offset-2">
                        <button class="btn-modal-close"
                                @click="$emit('close')">X</button>
                        <h1 class="title is-2 add-counter-title">Add new counter</h1>
                        <hr>
                        <p class="control">
                            <input class="input is-medium"
                                   type="number"
                                   v-model="format"
                                   :isFormatError="isFormatError"
                                   :placeholder="placeholderFormatMessage"
                                   :class="{ 'is-error animated shake': hasErrorFormat }">
                        </p>
                        <p class="control">
                            <input class="input is-medium"
                                   type="number"
                                   v-model="value"
                                   :disabled="disableInput"
                                   :isValueError="isValueError"
                                   :isFormatFilled="isFormatFilled"
                                   :placeholder="placeholderValueMessage"
                                   :class="{ 'is-error animated shake': hasErrorValue }">
                        </p>
                        <p class="control ctrl-btn">
                            <button class="button is-medium btn-add"
                                    @click="newCounterValues"
                                    :disabled="disableButton"
                                    :isAllFilled="isAllFilled">Add Counter</button>
                        </p>
                    </div>
                </div>

            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "NewCounterModal",
        data () {
            return {
                value: '',
                format: '',
                placeholderFormat: '',
                placeholderValue: '',
                hasErrorFormat: false,
                hasErrorValue: false,
                disableButton: true,
                disableInput: true
            }
        },

        computed: {
            placeholderFormatMessage () {
                if (!this.hasErrorFormat) {
                    return this.placeholderFormat = 'Type a format here.'
                } else {
                    let errorMessage = 'Type format from 0 to 4'
                    return this.placeholderFormat = errorMessage
                }
            },
            
            placeholderValueMessage () {
                if (!this.hasErrorValue) {
                    return this.placeholderValue = 'Type a number here.'
                } else {
                    if (this.format !== '') {
                        let number = Math.pow(10, Number(this.format)) - 1
                        let errorMessage = 'Type number from 0 to ' + number

                        return this.placeholderValue = errorMessage
                    } else {
                        return this.placeholderValue = 'Type format first!'
                    }
                    
                }
            },

            isFormatError () {
                if (this.format < 0 || this.format > 4) {
                    this.hasErrorFormat = true
                    this.format = ''
                    this.disableInput = true
                } else {
                    this.hasErrorFormat = false
                }
            },

            isFormatFilled () {
                if (this.format > 0 && this.format < 5 && !this.hasErrorFormat) {
                    this.disableInput = false
                }
            },

            isValueError () {
                if (this.value < 0 || this.value > Math.pow(10, this.format) - 1) {
                    this.hasErrorValue = true
                    this.value = ''
                    this.disableButton = true
                } else {
                    this.hasErrorValue = false
                }
            },

            isAllFilled () {
                if (this.value !== '' && this.format !== '' && !this.hasErrorValue) {
                    this.disableButton = false
                }
            }
        },

        methods: {
            newCounterValues () {
                this.$emit('newCounter', this.value, this.format)
            },
        },
        props: ["showModal"]
    }
</script>

<style>
    .ctrl-btn {
        text-align: center;
    }

    .btn-add:hover {
        background-color: #F5DA55;
    }

    .add-counter-title {
        color: #f6223f;
    }

    .btn-modal-close {
        border: none;
        font-size: 20px;
        outline: 0;
        position: fixed;
        right: 20px;
        top: 20px;
        background: none;
    }

    .btn-modal-close:hover {
        color: red;
    }
</style>