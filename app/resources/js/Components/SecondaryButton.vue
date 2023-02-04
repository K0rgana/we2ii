<script setup>
defineProps({
    type: {
        type: String,
        default: "button",
    },
});
</script>

<template>
    <button
        :type="type"
        class="inline-flex items-center px-4 py-2 bg-blue-300 border border-transparent rounded-md font-semibold text-xs text-gray-900 uppercase tracking-widest shadow-sm hover:bg-blue-200 focus:outline-none focus:ring-2 focus:ring-indigo-900 focus:ring-offset-2 disabled:opacity-25 transition ease-in-out duration-150"
    >
        <slot />
    </button>
</template>
