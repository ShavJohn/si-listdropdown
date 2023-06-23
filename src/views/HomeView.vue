<template>
    <div class="home-container">
        <draggable v-model="dropDowns" tag="div" :group="dropDowns" item-key="id">
            <template #item="{ element: dropDwon }">
                <customDropDown :isOpen="dropDwon.isOpen" :key="dropDwon.id">
                    <template #buttonContent>
                        <button class="drop-down-btn" @click="toggleDropDown(dropDwon.id)">
                            {{  dropDwon.text  }}
                            <font-awesome-icon icon="fa-solid fa-chevron-down" />
                        </button>
                    </template>
                    <template #searchInput>
                        <input type="text" placeholder="Search" v-model="searchQuery">
                    </template>
                    <template #menuItem>
                        <template  v-for="country in filteredCountries">
                            <li @click="dropDwon.text = country.text, refreshStorage(), dropDwon.isOpen = false" >
                                {{  country.text  }}
                            </li>
                        </template>
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
                dropDowns: [],
                disableAddDropDown: false,
                disableRemoveDropDown: false,
                searchQuery: '',
                countriesList: [
                    {
                        key: 'spain',
                        text: 'Spain'
                    },
                    {
                        key: 'france',
                        text: 'France'
                    },
                    {
                        key: 'germany',
                        text: 'Germany'
                    },
                    {
                        key: 'italy',
                        text: 'Italy'
                    },
                    {
                        key: 'greece',
                        text: 'Greece'
                    },
                    {
                        key: 'poland',
                        text: 'Poland'
                    },
                    {
                        key: 'norway',
                        text: 'Norway'
                    },
                    {
                        key: 'sweden',
                        text: 'Sweden'
                    },
                    {
                        key: 'denmark',
                        text: 'Denmark'
                    },
                    {
                        key: 'romania',
                        text: 'Romania'
                    },
                    {
                        key: 'iceland',
                        text: 'Iceland'
                    },
                    {
                        key: 'finland',
                        text: 'Finland'
                    },
                    {
                        key: 'irland',
                        text: 'Irland'
                    },
                    {
                        key: 'malta',
                        text: 'Malta'
                    },
                    {
                        key: 'estonia',
                        text: 'Estonia'
                    }
                ]
            }
        },
        computed: {
            filteredCountries() {
                if(!this.searchQuery.length) {
                    return this.countriesList.filter(cuntryObject => !this.dropDowns.some(dropDownObject => dropDownObject.text === cuntryObject.text))
                } else {
                    return this.countriesList.filter(countryObject => {
                        const matchCountry = countryObject.text.toLowerCase().includes(this.searchQuery.toLowerCase());
                        const existsInDropDown = this.dropDowns && this.dropDowns.some(dropDownObject => dropDownObject.text.toLowerCase() === countryObject.text.toLowerCase());
                        return matchCountry && !existsInDropDown;
                    });
                }
                
            }
        },
        watch: {
            'dropDowns.length' : function (val) {
                this.disableAddDropDown = val > 11 ? true : false
                
                this.disableRemoveDropDown = val < 3 ? true : false 
            }
        },
        methods: {
            refreshStorage(){
                localStorage.removeItem('dropDowns')
                localStorage.setItem('dropDowns', JSON.stringify(this.dropDowns))
            },
            toggleDropDown(id: number) {

                this.dropDowns.forEach(dropdown => {
                    dropdown.id === id ? dropdown.isOpen = !dropdown.isOpen : dropdown.isOpen = false
                });
            },
            addElementToArray() {

                let id = this.dropDowns.length ? this.dropDowns[this.dropDowns.length-1].id + 1 : 1

                let newArrayItem = {
                    id: id,
                    text: '',
                    isOpen: false
                }

                this.dropDowns.push(newArrayItem)

                this.refreshStorage()
            },
            remeoveElementFromArray(id: number) {
                this.dropDowns.forEach((dropdown, key) => {
                    if(dropdown.id === id) {
                        this.dropDowns.splice(key, 1)
                    }
                });
                this.refreshStorage()
            }
        },
        mounted() {
            if(!localStorage.getItem('dropDowns')) {
                let dropDownsDemoData = [
                    { 
                        id: 1,
                        text: 'Spain', 
                        isOpen: false
                    },
                    { 
                        id: 2,
                        text: 'France', 
                        isOpen: false
                    },
                    { 
                        id: 3,
                        text: 'Germany', 
                        isOpen: false
                    },
                    { 
                        id: 4,
                        text: 'Denmark', 
                        isOpen: false
                    },
                    { 
                        id: 5,
                        text: 'Malta', 
                        isOpen: false
                    },
                    { 
                        id: 6,
                        text: 'Estonia', 
                        isOpen: false
                    },
                ]

                this.dropDowns = dropDownsDemoData

                localStorage.setItem('dropDowns', JSON.stringify(dropDownsDemoData))
                
            } 
            else {
                this.dropDowns = JSON.parse(localStorage.getItem('dropDowns')!)
            }
        }

    })

</script>
