<script lang="ts" setup>
    const props = withDefaults(defineProps<{
        rating?: number,
        author?: string,
        author_position?: string,
        description?: string
    }>(),
    {
    
    })
</script>

<template>
    <div class="review-card">
        <div class="review-card__rating">
            <svg v-for="item in rating" width="32" height="32" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M14.6545 3.83947C15.2035 2.72018 16.799 2.72018 17.348 3.83947L20.5465 10.3609L27.7178 11.4095C28.9453 11.5889 29.4368 13.0959 28.5512 13.9646L23.3557 19.0605L24.5801 26.2443C24.7892 27.471 23.4999 28.4041 22.4 27.8223L16.0012 24.4372L9.60241 27.8223C8.50252 28.4041 7.21324 27.471 7.42232 26.2443L8.64679 19.0605L3.45128 13.9646C2.56569 13.0959 3.05719 11.5889 4.28462 11.4095L11.4559 10.3609L14.6545 3.83947Z" fill="#FFD230"/>
            </svg>
        </div>
        <div class="review-card__description">
            {{ description }}
        </div>
        <hr>
        <div class="review-card__title-block">
            <span>{{ author }}</span>
            {{ author_position }}
        </div>
    </div>
</template>

<style lang="scss">
    .review-card {
        @include df_fdc;
        gap: 2rem;
        padding: 5.5rem 2rem;
        border-radius: 1.25rem;
        border: 1px solid #525252;
        &__rating {
            @include df_ac;
            gap: 0.25rem;
            svg {
                height: 2rem;
                width: 2rem;
            }
        }
        &__description {
            font-size: 1.5rem;
            font-weight: 400;
            line-height: 110%;
            color: #525252;
        }
        &__title-block {
            @include df_fdc;
            gap: .25rem;
            font-size: 1.5rem;
            font-weight: 400;
            line-height: 110%;
            color: #525252;
            span {
                font-weight: 550;
                color: #000;
            }
        }
    }
</style>