<template>
    <div :class="['n-flex-row', 'n-align-center', 'n-position-relative']">
        <img v-for="(item,idx) in _items" :key="idx" :src="label?(item[label]+''):(item as string)" />
    </div>
</template>

<script setup lang="ts">
import {computed, PropType} from 'vue'
import {Item} from '../types'

const props = defineProps({
    items: {
        type: Array as PropType<(string | Item)[]>,
        default: ()=>[]
    },
    label: {
        type: String,
        default: ''
    },
    reverse: {
        type: Boolean,
        default: false
    },
    space: {
        type: String,
        default: '-8px'
    }
})

const _reverse = computed(() => {
    return props.reverse && parseInt(props.space) < 0
})
const _items = computed(() => {
    if (_reverse.value) {
        return props.items.slice().reverse()
    }
    return props.items
})
</script>