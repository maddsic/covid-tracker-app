
<template>
    <select @change="onChange()" v-model="selected" class="form-select mt-10 block w-full p-3 rounded">
        <option value="0">Select Country</option>
        <option v-for="country in countries" :key="country.ID">{{ country.Country }}</option>
    </select>
</template>



<script>
    export default {

        name: "selectCountry",
        props: ['countries'],

        data() {
            return {
                selected: 0
            }
        },

        methods: {
            onChange() {
                // checking if the country selected is equal to the country ID and then return the result.
                const country = this.country.find((item) => item.ID === this.selected)

                console.log(country)

                this.$emit('get-country', country)
        }
        }


    }


</script>