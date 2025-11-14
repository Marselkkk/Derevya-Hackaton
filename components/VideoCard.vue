<script lang="ts" setup>
    const props = withDefaults(defineProps<{
        url?: string,
        type?: string,
        title?: string,
        description?: string
    }>(),
    {
    
    });

    const videoPlay = ref(false);
    const videoRef = ref<HTMLVideoElement | null>(null);

    const toggleVideo = () => {
        if (!videoRef.value) return;

        if (videoPlay.value) {
            videoRef.value.pause();
            videoPlay.value = false;
        } else {
            videoRef.value.play()
                .then(() => {
                    videoPlay.value = true;
                })
                .catch(error => {
                    console.error('Ошибка воспроизведения видео:', error);
                });
        }
    };

    onUnmounted(() => {
        if (videoRef.value) {
            videoRef.value.pause();
        }
    });
</script>

<template>
    <div class="video-card">
        <div class="video-card__video-block">
            <video ref="videoRef" preload="metadata">
                <source src="/images/video-test.mp4" type="video/mp4"/>
            </video>
            <div class="video-button" @click.stop="toggleVideo">
                <svg width="48" height="48" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg" v-if="videoPlay">
                    <circle cx="24" cy="24" r="20" stroke="#497D00" stroke-width="3"/>
                    <path d="M16 19C16 18.0681 16 17.6022 16.1522 17.2346C16.3552 16.7446 16.7446 16.3552 17.2346 16.1522C17.6022 16 18.0681 16 19 16C19.9319 16 20.3978 16 20.7654 16.1522C21.2554 16.3552 21.6448 16.7446 21.8478 17.2346C22 17.6022 22 18.0681 22 19V29C22 29.9319 22 30.3978 21.8478 30.7654C21.6448 31.2554 21.2554 31.6448 20.7654 31.8478C20.3978 32 19.9319 32 19 32C18.0681 32 17.6022 32 17.2346 31.8478C16.7446 31.6448 16.3552 31.2554 16.1522 30.7654C16 30.3978 16 29.9319 16 29V19Z" stroke="#497D00" stroke-width="2"/>
                    <path d="M26 19C26 18.0681 26 17.6022 26.1522 17.2346C26.3552 16.7446 26.7446 16.3552 27.2346 16.1522C27.6022 16 28.0681 16 29 16C29.9319 16 30.3978 16 30.7654 16.1522C31.2554 16.3552 31.6448 16.7446 31.8478 17.2346C32 17.6022 32 18.0681 32 19V29C32 29.9319 32 30.3978 31.8478 30.7654C31.6448 31.2554 31.2554 31.6448 30.7654 31.8478C30.3978 32 29.9319 32 29 32C28.0681 32 27.6022 32 27.2346 31.8478C26.7446 31.6448 26.3552 31.2554 26.1522 30.7654C26 30.3978 26 29.9319 26 29V19Z" stroke="#497D00" stroke-width="2"/>
                </svg>
                <svg v-else width="48" height="48" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M33.7655 22.7127L21.4042 15.3254C19.9045 14.4291 18 15.5096 18 17.2567V30.744C18 32.4912 19.9045 33.5717 21.4043 32.6754L33.7655 25.2878C34.7395 24.7057 34.7395 23.2948 33.7655 22.7127ZM24 44C35.0457 44 44 35.0457 44 24C44 12.9543 35.0457 4 24 4C12.9543 4 4 12.9543 4 24C4 35.0457 12.9543 44 24 44ZM24 6.5C33.665 6.5 41.5 14.335 41.5 24C41.5 33.665 33.665 41.5 24 41.5C14.335 41.5 6.5 33.665 6.5 24C6.5 14.335 14.335 6.5 24 6.5Z" fill="#497D00"/>
                </svg>
            </div>
        </div>
        <div class="video-card__title-block">
            <span>Весенняя посадка деревьев 2024 года — обзор с воздуха</span>
            Захватывающие кадры с воздуха: волонтеры высаживают 45 000 деревьев на площади 32 гектара.
        </div>
    </div>
</template>

<style lang="scss">
    .video-card {
        @include df_fdc;
        border-radius: 1.25rem;
        border: 1px solid #D4D4D8;
        overflow: hidden;
        &__video-block {
            height: 17.5rem;
            position: relative;
            .video-button {
                position: absolute;
                top: 50%;
                left: 50%;
                transform: translate(-50%, -50%);
                height: 3rem;
                width: 3rem;
                aspect-ratio: 1 / 1;
                svg {
                    @include wh-100;
                }
            }
            video {
                @include image_cover;
            }
        }
        &__title-block {
            @include df_fdc;
            padding: 2.5rem 3.875rem 2.5rem 2.5rem;
            background-color: #fff;
            font-size: 1.5rem;
            line-height: 110%;
            font-weight: 400;
            color: #27272A;
            @include mobile {
                font-size: 0.83rem;
                padding: 1.1667rem 3.33rem 1.1667rem 1.1667rem;
            }
            span {
                font-size: 1.5rem;
                line-height: 110%;
                font-weight: 500;
                color: #000;
                @include mobile {
                    font-size: 0.83rem;
                }
            }
        }
    }
</style>