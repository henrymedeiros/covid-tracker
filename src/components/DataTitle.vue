<template>
    <div>
        <h2>{{title}}</h2>
        <div>
            {{timestamp}}
        </div>
    </div>
</template>
<script>
import moment from 'moment';
export default {
    name: 'DataTitle',
    props: ['title', 'dataDate'],
    computed: {
        timestamp: function(){
            return moment(this.dataDate).format('MMMM Do YYYY, h:mm:ss a')
        }
    }
}
</script>
<style scoped>
    
</style>