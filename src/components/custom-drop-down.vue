<template>
    <div class="drop-down-container" draggable="true">
        <div class="drop-dwon-button-container">
            <button class="drop-down-btn" @click="openDropDown = !openDropDown">
                <slot name="buttonContent">

                </slot>
                <font-awesome-icon icon="fa-solid fa-chevron-down" />
            </button>
            <button class="delete-btn"><font-awesome-icon icon="fa-solid fa-xmark" /></button>
        </div>
        <div class="drop-down-manu-container" :class="openDropDown ? 'drop-down-open' : 'drop-down-close'">
            <div class="drop-down-search-input">
                <input type="text">
            </div>
            <ul>
                <li v-for="listItem in listItems">
                    {{  listItem.value  }}
                </li>
            </ul>
        </div>
    </div>
</template>

<script lang="ts">
    import { defineComponent } from "vue";

    export default defineComponent({
        data() {
            return {
                openDropDown: false,
                listItems: [
                    {
                        key: 'id',
                        value: 'Id'
                    },
                    {
                        key: 'title',
                        value: 'Title'
                    },
                    {
                        key: 'id',
                        value: 'Id'
                    },
                    {
                        key: 'title',
                        value: 'Title'
                    },
                    {
                        key: 'id',
                        value: 'Id'
                    },
                    {
                        key: 'title',
                        value: 'Title'
                    }
                ]
            }
        },
        methods: {
            
        }

    })
</script>