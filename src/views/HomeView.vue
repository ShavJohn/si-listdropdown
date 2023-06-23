<template>
    <div>
        <button @click="change">Click</button>
        {{  someData  }}
    </div>
</template>

<script lang="ts">
    import { defineComponent } from "vue";

    export default defineComponent({
        data() {
            return {
                someData: ''
            }
        },
        methods: {
            change() {
                this.someData = 'Some news'
            }
        }

    })

</script>
