<template>
    <div class="home-container">
        <draggable v-model="dropDwons" tag="div" :group="dropDwons" item-key="id">
            <template #item="{ element: dropDwon }">
                <customDropDown :isOpen="dropDwon.isOpen" :key="dropDwon.id">
                    <template #buttonContent>
                        <button class="drop-down-btn" @click="toggleDropDown(dropDwon.id)">
                            {{  dropDwon.title  }}
                            <font-awesome-icon icon="fa-solid fa-chevron-down" />
                        </button>
                    </template>
                    <template #deleteBtn> 
                        <button v-if="!disableRemoveDropDown" @click="remeoveElementFromArray(dropDwon.id)" class="delete-btn"><font-awesome-icon icon="fa-solid fa-xmark" /></button>
                    </template>
                </customDropDown>
            </template>
        </draggable>
        <button v-if="!disableAddDropDown" @click="addElementToArray" class="add-drop-down-btn">
            <font-awesome-icon icon="fa-solid fa-plus" />
            Add
        </button>
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
                dropDwons: [],
                disableAddDropDown: false,
                disableRemoveDropDown: false
            }
        },
        watch: {
            'dropDwons.length' : function (val) {
                console.log(val)
                this.disableAddDropDown = val > 11 ? true : false
                
                this.disableRemoveDropDown = val < 3 ? true : false 
            }
        },
        methods: {
            toggleDropDown(id: number) {

                this.dropDwons.forEach(dropdown => {
                    dropdown.id === id ? dropdown.isOpen = !dropdown.isOpen : dropdown.isOpen = false
                });
            },
            addElementToArray() {
                localStorage.removeItem('dropDwons')

                let id = this.dropDwons.length ? this.dropDwons[this.dropDwons.length-1].id + 1 : 1

                let newArrayItem = {
                    id: id,
                    text: '',
                    isOpen: false
                }

                this.dropDwons.push(newArrayItem)

                localStorage.setItem('dropDwons', JSON.stringify(this.dropDwons))
            },
            remeoveElementFromArray(id: number) {
                localStorage.removeItem('dropDwons')
                this.dropDwons.forEach((dropdown, key) => {
                    if(dropdown.id === id) {
                        this.dropDwons.splice(key, 1)
                    }
                });
                localStorage.setItem('dropDwons', JSON.stringify(this.dropDwons))
            }
        },
        mounted() {
            if(!localStorage.getItem('dropDwons')) {
                let dropDwonsDemoData = [
                    { 
                        id: 1,
                        text: 'Id', 
                        isOpen: false
                    },
                    { 
                        id: 2,
                        text: '', 
                        isOpen: false
                    },
                    { 
                        id: 3,
                        text: 'Id', 
                        isOpen: false
                    },
                    { 
                        id: 4,
                        text: '', 
                        isOpen: false
                    },
                    { 
                        id: 5,
                        text: 'Id', 
                        isOpen: false
                    },
                    { 
                        id: 6,
                        text: '', 
                        isOpen: false
                    },
                ]

                this.dropDwons = dropDwonsDemoData

                localStorage.setItem('dropDwons', JSON.stringify(dropDwonsDemoData))
                
            } 
            else {
                this.dropDwons = JSON.parse(localStorage.getItem('dropDwons')!)
            }
        }

    })

</script>
