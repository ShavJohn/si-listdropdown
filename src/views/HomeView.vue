<template>
    <div class="home-container">
        <draggable v-model="dropDwons" tag="div" :group="dropDwons" item-key="id">
            <template #item="{ element: dropDwon }">
                <customDropDown>
                    <template #buttonContent>
                        {{  dropDwon  }}
                    </template>
                </customDropDown>
            </template>
        </draggable>
    </div>
</template>

<script lang="ts">
    import { defineComponent } from "vue";
    import customDropDown from '../components/custom-drop-down.vue';
    import draggable from 'vuedraggable';

    export default defineComponent({
        components: {customDropDown, draggable},
        data() {
            return {
                dropDwons: [
                    'drop1',
                    'drop2',
                    'drop1',
                    'drop2',
                    'drop1',
                    'drop2'
                ]
            }
        },
        methods: {

        }

    })

</script>
