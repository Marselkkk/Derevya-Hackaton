<script lang="ts" setup>
    import IMask from 'imask';

    const props = defineProps<{
        placeholder?: string,
        maxLength?: number,
        name?: string,
        id?: string,
        state?: 'active' | 'disabled' | 'error',
        onInput?: Function,
        mask?: string,
        modelValue?: string,
        error?: string,
        title?: string
    }>();

    const emit = defineEmits<{
        (e: 'update:modelValue', value: string): void
    }>();
    let localValue = ref(props.modelValue || '');
    const inputRef = ref(null);

    const handleInput = (event: Event) => {
        const target = event.target as HTMLInputElement;
        let value = target.value;

        if (props.name === 'phone' && value.length > 16) {
            value = value.slice(0, 16);
            target.value = value;   
        }
        localValue.value = value;
        emit('update:modelValue', localValue.value);

        if (props.onInput) props.onInput(event);
    };

    watch(() => props.modelValue, (newVal) => {
        if (newVal !== localValue.value) {
            localValue.value = newVal || '';
        }
    });

    onMounted(() => {
        if (inputRef.value && props.name === 'phone') {
            IMask(inputRef.value as HTMLInputElement, {
                mask: '+{7} 000 000-00-00',
                prepare: (str, masked) => {
                    if (masked.value.length === 0 && str === '8') {
                        return '7';
                    }
                    return str;
                },
                max: 16
            });
        } else if (props.mask && inputRef.value) {
            IMask(inputRef.value as HTMLInputElement, { mask: props.mask });
        }
    });



</script>

<template>
    <div class="field">
        <span>{{ title }}</span>
        <label class="input-label"
        :for="id">
            <input type="text"
            :name="name"
            :id="id"
            @input="handleInput"
            ref="inputRef"
            :max-length="maxLength"
            :placeholder="placeholder">
        </label>
        <div class="field__error" v-if="error">
            {{ error }}
        </div>
    </div>
</template>

<style scoped lang="scss">
    input[type="text"],
    textarea {
        background-color: unset;
        width: 100%;
        outline: unset;
        border: unset;
        padding: 0;
        font-family: "Montserrat", sans-serif;
        font-size: 1.5rem;
        font-weight: 300;
        line-height: 110%;
        resize: none;
        &::placeholder {
            @include transition(color);
        }
    }
    textarea {
        height: 7.125rem;
    }
    .field {
        @include df_fdc;
        gap: .5rem;
        span {
            font-size: 1.5rem;
            font-weight: 400;
            line-height: 110%;
            color: #000;
        }
        &__error {
            font-size: 1.5rem;
            font-weight: 250;
            line-height: 110%;
            color: #000;
            display: none;
        }
        .input-label {
            position: relative;
            padding: 1.125rem 1.25rem;
            background-color: #F5F5F5;
            border-radius: 2rem;
        }
        &:has(.error) {
            .field__error {
                display: block;
            }
        }
    }
</style>