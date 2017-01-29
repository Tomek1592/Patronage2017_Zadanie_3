<template>
    <div class="modal" :class="{ 'is-active': showModal }">
        <div class="modal-background" 
             @click="$emit('close')"></div>
        <div class="modal-content animated slideInDown">
            <div class="box">
                <div class="columns">
                    <div class="column is-10 is-offset-1">
                        <button class="btn-modal-close" 
                                @click="$emit('close')">X</button>
                        <h1 class="title is-3">Value of <span class="counter-name">Score {{ id }}:</span></h1>
                        <hr>
                        <p class="value">{{ value }}</p>
                    </div>
                </div>

            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "GetModal",
        data () {
            return {
                id: this.currentId,
                value: this.currentValue
            }
        },
        props: ["showModal", "currentId", "currentValue"]
    }
</script>

<style>
    .value {
        font-size: 150px;
        color: black;
    }

    .counter-name {
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