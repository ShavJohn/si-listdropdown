<template>
    <div class="drop-down-container">
        <font-awesome-icon class="drag-btn" icon="fa-solid fa-grip-vertical" />
        <div class="drop-down-inner-container" draggable="true">
            <div class="drop-dwon-button-container">
                <slot name="buttonContent"></slot>
            </div>
            <div class="drop-down-manu-container" :class="isOpen ? 'drop-down-open' : 'drop-down-close'">
                <div class="drop-down-search-input">
                    <slot name="searchInput"></slot>
                </div>
                <ul>
                    <slot name="menuItem"></slot>
                </ul>
            </div>
        </div>
        <slot name="deleteBtn"></slot>
    </div>
</template>

<script lang="ts">
    import { defineComponent } from "vue";

    export default defineComponent({
        props: {
            isOpen: {
                required: true
            }
        },

    })
</script>