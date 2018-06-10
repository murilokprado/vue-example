<template>
    <button @click="triggerAction()" class="button" :class="styleOfButtonS" :type="type">{{title}}</button>
</template>

<script>
export default {
    props: {
        type: {
            required: true,
            type: String
        },
        title: {
            required: true,
            type: String
        },        
        confirmation: {
            required: false,
            type: Boolean
        },
        styleButton: {
            required: false,
            type: String
        }                
    },
    methods: {
        triggerAction() {
            if(this.confirmation) {
                if(confirm("Confirma remove ? ")) {
                    this.$emit('buttonActive');
                }
            }
            this.$emit('buttonActive');
        }
    },
    computed: {
        styleOfButtonS() {
            let styleOfButton;
            switch(this.styleButton) {
                case 'standard': 
                    styleOfButton = 'button-standard';
                    break;
                case 'warning': 
                    styleOfButton = 'button-warning';
                    break;
                default:
                    styleOfButton = 'button-standard';
                    break;             
            }
            return styleOfButton;
        }
    }
}
</script>

<style>
.button {
    display: inline-block;
    padding: 10px;
    border-radius: 3px;
    margin: 10px;
    font-size: 1.2em;
}

.button-warning {
    background: firebrick;
    color: white;
}

.button-standard {
    background: darkcyan;
    color: white;
}
</style>
