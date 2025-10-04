<template>
    <Transition name="fade">
        <div v-show="modalActive">
            <div class="overflow-y-auto overflow-x-hidden fixed inset-0 z-50 flex justify-center items-center">
                <slot />
            </div>
        </div>
    </Transition>
    
</template>
<script>
import { Transition } from 'vue';

export default {
    props: ['modalActive']
}

</script>