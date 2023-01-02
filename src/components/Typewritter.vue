<template>
    <code class="typewriter text-bookmark-grey text-lg text-center lg:text-left mb-6">{{ text }}</code>
</template>
  
<script>
import { ref, computed, watchEffect, onMounted } from 'vue'


export default {
    props: {
        texts: {
            type: Array,
            required: true
        }
    },
    setup(props) {
        const text = ref('')
        const index = ref(0)
        const currentText = ref(props.texts[index.value])

        const startTypewriter = () => {
            const interval = setInterval(() => {
                text.value = currentText.value.slice(0, index.value + 1)
                index.value++
                if (index.value === currentText.value.length) {
                    clearInterval(interval)
                    index.value = 0
                    currentText.value = props.texts[(index.value + 1) % props.texts.length]
                }
            }, 100)
        }

        watchEffect(() => {
            console.log('currentText', currentText.value);
            if (currentText) {
                startTypewriter()
            }



        }, { deep: true })

        // onMounted(() => {
        //     startTypewriter()
        // })

        return {
            text
        }
    }
}
</script>