<template>
    <div>
        <app-header></app-header>
        <router-view :key="$route.fullPath"></router-view>
    </div>
</template>

<script>
import AppHeader from '@/components/settings/appHeader.vue'
export default {
    components:{
        AppHeader
    },
    data()
    {
        return{

        }
    }
}
</script>