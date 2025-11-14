<script lang="ts" setup>
    const { currentlyMobile } = mobileState();

    const header = ref<HTMLElement>()
    let lastScrollY = ref(0)
    let isScrolling = ref(false)

    const burgerOpen = ref(false);

    const toggleMenu = () => {
        burgerOpen.value = !burgerOpen.value;

        if (process.client) {
            if (burgerOpen.value) {
                document.body.style.overflow = 'hidden';
            } else {
                document.body.style.overflow = '';
            }
        }
    }

    const handleScroll = () => {
        if (!header.value) return
        
        const currentScrollY = window.scrollY
        
        if (currentScrollY <= 0) {
            header.value.style.transform = 'translateY(0)'
            return
        }
        
        if (currentScrollY > lastScrollY.value && currentScrollY > 100) {
            header.value.style.transform = 'translateY(-100%)'
        } else if (currentScrollY < lastScrollY.value) {
            header.value.style.transform = 'translateY(0)'
        }
        
        lastScrollY.value = currentScrollY
    }

    const throttleScroll = () => {
        if (!isScrolling.value) {
            window.requestAnimationFrame(() => {
            handleScroll()
            isScrolling.value = false
            })
            isScrolling.value = true
        }
    }

    onMounted(() => {
        lastScrollY.value = window.scrollY
        window.addEventListener('scroll', throttleScroll, { passive: true })
    })

    onUnmounted(() => {
        window.removeEventListener('scroll', throttleScroll)
    });

</script>

<template>
    <header ref="header">
        <div class="header-section">
            <div class="header-section__container">
                <div class="header-section__logo">
                    <div class="header-section__logo__img">
                        <svg width="42" height="42" viewBox="0 0 42 42" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <path d="M21 0C16.6816 0 13.0351 2.62766 11.8555 6.23378C7.29988 6.89686 3.81818 10.513 3.81818 14.8752C3.81818 15.702 3.94365 16.5034 4.17848 17.2635C1.65819 18.8371 0 21.4903 0 24.5003C0 29.3329 4.27365 33.2505 9.54545 33.2505H15.2727V38.5C15.2727 40.433 16.9822 42 19.0909 42H22.9091C25.0178 42 26.7273 40.433 26.7273 38.5V33.2505H32.4545C37.7264 33.2505 42 29.3329 42 24.5003C42 21.4903 40.3418 18.8371 37.8215 17.2635C38.0564 16.5034 38.1818 15.702 38.1818 14.8752C38.1818 10.513 34.7001 6.89686 30.1445 6.23378C28.9649 2.62766 25.3184 0 21 0ZM23.8636 33.2505V38.5C23.8636 38.9832 23.4363 39.375 22.9091 39.375H19.0909C18.5637 39.375 18.1364 38.9832 18.1364 38.5V33.2505H23.8636ZM14.4208 7.67336C14.9751 4.80417 17.7114 2.62504 21 2.62504C24.2886 2.62504 27.0249 4.80417 27.5792 7.67336C27.6962 8.27943 28.257 8.72952 28.9279 8.75582C32.4823 8.89517 35.3182 11.582 35.3182 14.8752C35.3182 15.7467 35.1205 16.5724 34.7654 17.3194C34.4611 17.9594 34.7566 18.7056 35.4377 19.0178C37.6335 20.0241 39.1364 22.1025 39.1364 24.5003C39.1364 27.8831 36.1448 30.6254 32.4545 30.6254H9.54545C5.85519 30.6254 2.86364 27.8831 2.86364 24.5003C2.86364 22.1025 4.36645 20.0241 6.56233 19.0178C7.24344 18.7056 7.53886 17.9594 7.23464 17.3194C6.8795 16.5724 6.68182 15.7467 6.68182 14.8752C6.68182 11.582 9.51769 8.89517 13.0721 8.75582C13.743 8.72952 14.3038 8.27943 14.4208 7.67336Z" fill="#2A521E"/>
                        </svg>
                    </div>
                    <span>
                        Derev'Ya
                    </span>
                </div>
                <nav class="header-section__nav-block" v-if="!currentlyMobile">
                    <ul>
                        <li>
                            <ElementLink link="#history">
                                История
                            </ElementLink>
                        </li>
                        <li>
                            <ElementLink link="#video">
                                Видео
                            </ElementLink>
                        </li>
                        <li>
                            <ElementLink link="#forest">
                                Статистика
                            </ElementLink>
                        </li>
                        <li>
                            <ElementLink link="#about">
                                Как это работает
                            </ElementLink>
                        </li>
                        <li>
                            <ElementLink link="#feedback">
                                Зарегестрируйтесть сейчас
                            </ElementLink>
                        </li>
                    </ul>
                </nav>
                <div class="header-section__burger-button"
                @click="toggleMenu" 
                v-if="currentlyMobile"
                :data-active="burgerOpen">
                    <div></div>
                    <div></div>
                    <div></div>
                </div>
            </div>
            <div class="header-section__menu" v-if="burgerOpen && currentlyMobile">
                <nav>
                    <ul>
                        <li>
                            <a href="#hero"
                            @click="toggleMenu">Домой</a>
                        </li>
                        <li>
                            <a href="#history"
                            @click="toggleMenu">История</a>
                        </li>
                        <li>
                            <a href="#video"
                            @click="toggleMenu">Видео</a>
                        </li>
                        <li>
                            <a href="#forest"
                            @click="toggleMenu">Статистика</a>
                        </li>
                        <li>
                            <a href="#about"
                            @click="toggleMenu">Как это работает</a>
                        </li>
                        <li>
                            <a href="#feedback"
                            @click="toggleMenu">Зарегистрируйтесь сейчас</a>
                        </li>
                    </ul>
                </nav>
                <a href="#feedback" class="button"
                @click="toggleMenu">
                    Присоединиться к мероприятию
                </a>
            </div>
        </div>
    </header>
</template>

<style lang="scss">
    header {
        position: fixed;
        z-index: 100;
        top: 0;
        left: 0;
        transform: translateY(0);
        transition: transform 0.3s ease;
        width: 100%;
    }

    .header-section {
        position: relative;
        &__container {
            padding: 1.25rem 4rem;
            background-color: #fff;
            @include df_jb_ac;
            @include mobile {
                padding: 0.4167rem 1.6667rem;
            }
        }
        &__logo {
            @include df_ac;
            gap: 1.25rem;
            &__img {
                max-height: 2.625rem;
                aspect-ratio: 1 / 1;
                height: 100%;
                @include mobile {
                    max-height: 2.33rem;
                }
                svg {
                    @include wh-100;
                }
            }
            span {
                font-size: 2rem;
                line-height: 110%;
                font-weight: 400;
                color: #2A521E;
                font-size: 1rem;
            }
        }
        &__nav-block {
            ul {
                @include df_ac;
                gap: 3.75rem;
            }
        }
        &__burger-button {
            @include df_fdc;
            gap: .33rem;
            div {
                height: .25rem;
                width: 2rem;
                background-color: #525252;
                @include transition(transform);
            }
            &[data-active="true"] {
                div:nth-child(1) {
                    transform: translateY(0.5rem) rotate(45deg);
                }
                
                div:nth-child(2) {
                    opacity: 0;
                    transform: scale(0);
                }
                
                div:nth-child(3) {
                    transform: translateY(-0.625rem) rotate(-45deg);
                }
            }
        }
        &__menu {
            position: fixed;
            top: 3rem;
            left: 0;
            width: 100%;
            padding: 0.8333rem;
            background-color: #fff;
            @include df_fdc;
            gap: 2.33rem;
            nav {
                ul {
                    @include df_fdc;
                    gap: 2.5rem;
                    li {
                        a {
                            font-size: 1rem;
                            font-weight: 400;
                            line-height: 110%;
                            color: #525252;
                        }
                    }
                }
            }
            .button {
                padding: 1rem;
                background-color: #5EA500;
                border-radius: 5px;
                width: 100%;
                color: #fff;
                font-size: 0.9167rem;
                font-weight: 400;
                line-height: 110%;
            }
        }
    }
</style>