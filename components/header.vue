<script lang="ts" setup>
    const header = ref<HTMLElement>()
    let lastScrollY = ref(0)
    let isScrolling = ref(false)

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
    })
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
                <nav class="header-section__nav-block">
                    <ul>
                        <li>
                            <ElementLink>
                                История
                            </ElementLink>
                        </li>
                        <li>
                            <ElementLink>
                                Видео
                            </ElementLink>
                        </li>
                        <li>
                            <ElementLink>
                                Статистика
                            </ElementLink>
                        </li>
                        <li>
                            <ElementLink>
                                Как это работает
                            </ElementLink>
                        </li>
                        <li>
                            <ElementLink>
                                Зарегестрируйтесть сейчас
                            </ElementLink>
                        </li>
                    </ul>
                </nav>
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
        &__container {
            padding: 1.25rem 4rem;
            background-color: #fff;
            @include df_jb_ac;
        }
        &__logo {
            @include df_ac;
            gap: 1.25rem;
            &__img {
                max-height: 2.625rem;
                aspect-ratio: 1 / 1;
                height: 100%;
                svg {
                    @include wh-100;
                }
            }
            span {
                font-size: 2rem;
                line-height: 110%;
                font-weight: 400;
                color: #2A521E;
            }
        }
        &__nav-block {
            ul {
                @include df_ac;
                gap: 3.75rem;
            }
        }
    }
</style>