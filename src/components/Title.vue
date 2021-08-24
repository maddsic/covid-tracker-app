<template>
    <div class="text-center">
        <h2 class="text-3xl font-bold">{{ text }}</h2>
        <div class="text-2xl mt-4 mb-10">
            <!-- injecting the timestamp -->
            {{ timestamp }}
        </div>
    </div>
</template>


<script>
// importing moment js
import moment from 'moment'
    export default {
        name: 'Title',
        props: ['text', 'dataDate'],

        // formatting our date and time using moment.js
        computed: {
            timestamp: function() {
                return moment(this.dataDate).format('MMMM Do YYYY, h:mm:ss a')
            }
        }
    }
</script>