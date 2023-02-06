<script setup>
import { useForm } from "@inertiajs/vue3";
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import SecondaryButton from "@/Components/SecondaryButton.vue";
import TextInput from "@/Components/TextInput.vue";

const props = defineProps({
    game: {},
});

const form = useForm({
    name: props.game.name,
    platform: props.game.platform,
    genre: props.game.genre,
    release: props.game.release,
});

const updateGame = () => {
    form.patch(route("game.update", props.game.id), {
        onFinish: () => {
            alert("Success! Game Updated.");
        },
    });
};
</script>

<template>
    <AuthenticatedLayout>
        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <h1 class="p-6 text-gray-900">Update the Game</h1>

                    <form @submit.prevent="updateGame" class="p-6">
                        <div class="justify-between items-center">
                            <label>Name</label>
                            <TextInput
                                type="text"
                                class="block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                                required
                                autofocus
                                v-model="form.name"
                            />

                            <label>Platform</label>
                            <TextInput
                                type="text"
                                class="block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                                required
                                autofocus
                                v-model="form.platform"
                            />

                            <label>Genre</label>
                            <TextInput
                                type="text"
                                class="block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                                required
                                autofocus
                                v-model="form.genre"
                            />

                            <label>Release</label>
                            <TextInput
                                type="date"
                                class="block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                                required
                                autofocus
                                v-model="form.release"
                            />
                        </div>

                        <SecondaryButton class="my-2" type="submit"
                            >Save</SecondaryButton
                        >
                    </form>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
