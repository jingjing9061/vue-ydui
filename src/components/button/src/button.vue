<template>
    <button @click="handleClick" :disabled="disabled" :class="classes" :style="{backgroundColor: bgcolor, color: color}" :type="actionType">
        <slot></slot>
    </button>
</template>

<script type="text/babel">
    import {isColor} from '../../../utils/assist';

    export default {
        name: 'yd-button',
        props: {
            disabled: Boolean,
            actionType: {
                validator(value) {
                    return ['button', 'submit', 'reset'].indexOf(value) > -1;
                },
                default: 'button'
            },
            type: {
                validator(value) {
                    return ['primary', 'danger', 'warning', 'hollow', 'disabled'].indexOf(value) > -1;
                },
                default: 'primary'
            },
            size: {
                validator(value) {
                    return ['small', 'large'].indexOf(value) > -1;
                }
            },
            bgcolor: {
                validator(value) {
                    if (!value) return true;
                    return isColor(value);
                }
            },
            color: {
                validator(value) {
                    if (!value) return true;
                    return isColor(value);
                }
            },
            shape: {
                validator(value) {
                    return ['square', 'circle'].indexOf(value) > -1;
                },
                default: 'square'
            }
        },
        computed: {
            classes() {
                let s = this.size === 'large' ? 'yd-btn-block' : 'yd-btn';
                let b = 'yd-btn-' + this.type;
                if (this.disabled) {
                    b = 'yd-btn-disabled';
                }

                if (this.bgcolor) {
                    b = '';
                }
                return s + ' ' + b + (this.shape === 'circle' ? ' yd-btn-circle' : '');
            }
        },
        methods: {
            handleClick(evt) {
                this.$emit('click', evt);
            }
        }
    }
</script>

<style lang="less">
    @import '../../../styles/components/button.less';
</style>
