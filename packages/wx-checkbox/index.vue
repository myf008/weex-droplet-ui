<template>
    <div class="wx-checkbox" @click="handleClick">
        <text v-if="align === 'left'" 
            class="wx-text align-left">{{ text }}</text>
        <!-- CheckBox -->
        <div class="wx-box" :style="{'border-color':checked ? checkedColor : '#DCDCDC'}">
            <div v-if="checked" class="checked" :style="{'border-right-color': checkedColor, 'border-bottom-color': checkedColor}"></div>
        </div>
        <text v-if="align === 'right'" 
            class="wx-text align-right">{{ text }}</text>
    </div>
</template>
<style scoped>
    .wx-checkbox {
        flex-direction: row;
        align-items: center;
    }

    .wx-text {
        font-size: 32px;
    }
    .align-right {
        padding-left: 16px;
    }
    .align-left {
        padding-right: 16px;
    }

    .wx-box {
        width: 44px;
        height: 44px;
        border-width: 1px;
        border-style: solid;
        border-color: #DCDCDC;
        background-color: #fff;
        border-radius: 4px;
    }

    .checked {
        position: absolute;
        top: 6px;
        left: 14px;
        z-index: 100;
        width: 14px;
        height: 24px;
        border-bottom-width: 2px;
        border-bottom-style: solid;
        /*border-bottom-color: #027FF3;*/
        border-right-width: 2px;
        border-right-style: solid;
        /*border-right-color: #027FF3;*/
        transform: rotate(45deg);
    }

</style>
<script>
    export default {
        props: {
            defaultChecked: {
                type: Boolean,
                default: false
            },
            disabled: {
                type: Boolean,
                default: false
            },
            text: {
                type: String,
                default: ''
            },
            align: {
                type: String,
                // left or right
                default: 'left' 
            },
            checkedColor: {
                type: String,
                default: '#027FF3' 
            },
        },

        data () {
            return {
                checked: false,
            }
        },

        created () {
            this.checked = this.defaultChecked;
        },

        methods: {
            handleClick () {
                if (this.disabled) return;
                this.checked = !this.checked;
                this.$emit('input', this.checked);
                this.$emit('wxChange', this.checked);
            },
        }
    }
</script>