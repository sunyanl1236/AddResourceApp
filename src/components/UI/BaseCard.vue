<template>
<!-- just is a wrapper with a certain look, don't have logic -->
    <div>
        <!-- don't need to give this slot name, because it's the only slot -->
        <slot></slot>
    </div>
</template>

<style scoped>
    div {
    border-radius: 12px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    padding: 1rem;
    margin: 2rem auto;
    max-width: 40rem;
    }
</style>