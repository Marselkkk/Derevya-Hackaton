<script lang="ts" setup>
    const props = withDefaults(defineProps<{
        link?: string,
    }>(),
    {
        link: '#'
    })
</script>

<template>
    <a v-if="link" 
    class="link"
    :href="link">
        <slot />
    </a>
</template>

<style lang="scss">
    .link {
        @include df_ac_jcc;
        width: fit-content;
        text-wrap: nowrap;
        cursor: pointer;
        @include transition(color, border-color, background-color);

        box-sizing: border-box;
        -moz-box-sizing: border-box;
        -webkit-box-sizing: border-box;

        font-size: 1.5rem;
        line-height: 100%;
        font-weight: 400;

        color: #2A521E;
        padding: .5rem 1rem;
        
        position: relative;
        text-decoration: none;
        @include mobile {
            font-size: 1rem;
        }
        
        &::after {
            content: '';
            position: absolute;
            width: 0;
            height: 2px;
            bottom: 0;
            left: 0;
            background-color: #2A521E;
            transition: width 0.3s ease;
        }
        
        &:hover::after {
            width: 100%;
        }
    }
</style>