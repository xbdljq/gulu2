<template>
    <!--@click="$emit('click')"-->
    <button class="g-button" :class="{[`icon-${iconPosition}`]: true}" @click="$emit('click')" >
        <g-icon class="icon" :name="icon" v-if="icon && !loading"></g-icon>
        <g-icon class="loading icon" name="loading" v-if="loading"></g-icon>
        <div class="content">
            <slot></slot>
            <!--<slot/>-->
        </div>

    </button>
</template>
<script>
//import Vue from 'vue'

    import Icon from './icon'
  //  Vue.component('g-icon',Icon)
    export default {
        components: {
            'g-icon': Icon
        },
        props: {
            icon: {},
            loading: {
                type: Boolean,
                default:false
            },
            iconPosition: {
                type: String,
                default: 'left',
                validator: function(value){  //属性检查器
                    return value === 'left' || value === 'right'
                }
            }
        }
    }
</script>
<style lang="scss">
    @keyframes spin {
        0%{transform: rotate(0deg);}
        100%{transform: rotate(360deg)}
    }
    .g-button{
        font-size: var(--font-size);height: var(--button-height);
        border-radius: var(--border-radius);background: var(--button-bg);border:1px solid var(--border-color);
        display: inline-flex;justify-content: center;align-items: center;
        vertical-align: middle;padding: 0 1em;

        &:hover{border-color:var(--border-color-hover);}
        &:active{background-color:var(--button-active-bg);}
        &:focus{outline: none;}
        > .content{order:2}
        > .icon{order:1; margin-right: .1em}

        &.icon-right{
            > .content{order:1;}
            > .icon{order:2; margin-left: .1em; margin-right: 0;}
        }
        .loading{
            -webkit-animation: spin 2s infinite linear;
            -o-animation: spin 2s infinite linear;
            animation: spin 2s infinite linear;
        }
    }

</style>