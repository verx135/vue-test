<template>
    <div class="dialog" v-if="show" @click.stop="hideDialog">
        <div @click.stop class="dialog_content">
            <slot></slot>
        </div>
    </div>
</template>

<script>
import toggleMixin from '@/mixins/toggleMixin';

export default {
    name: 'MyDialog',
    mixins: [toggleMixin],
    mounted() {
        console.log('dialog mounted');
    }
}
    // props: {
    //     show: {
    //         type: Boolean,
    //         default: false
    //     }
    // },
    //     methods: {
    //         hideDialog() {
    //             this.$emit('update:show', false)
    //         }
    //     }
    // }
</script>

<style>
.dialog {
    top: 0;
    bottom: 0;
    right: 0;   
    left: 0;
    background: rgba(0, 0, 0, 0.5);  
    position: fixed;
    display: flex;
}

.dialog_content {
    margin: auto;
    background: white;
    border-radius: 12px;
    min-height: 50px;
    min-width: 300px;
    padding: 20px;
}
</style>