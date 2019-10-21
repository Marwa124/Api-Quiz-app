<template>
    <div class="service">
        <h2>This is the services page</h2>
        <app-header></app-header>
        <div slot="testing">{{ title }}</div>
    </div>
</template>


<script>

import AppHeader from '@/components/AppHeader';

export default {
    name: 'service',
    components: {
        AppHeader
    },
    data: function(){
        return{
        title: "this is Our Slot"
        }
    }
}
</script>

<style lang="scss">
    h2{
        color: red;
        cursor: pointer;
    }
</style>>
