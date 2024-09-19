<template>
    <div>
        <header class="bg-light p-3 mb-4">
            <div class="container">
                <BarraNav /> 
            </div>
        </header>
        <router-view />
    </div>
</template>

<script setup>
    import BarraNav from './components/BarraNav.vue';

</script>

<style>
    header {
        background-color: #f8f9fa;
    }
</style>