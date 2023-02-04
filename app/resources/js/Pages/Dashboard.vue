<script setup>
import SecondaryButton from "@/Components/SecondaryButton.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import TextInput from "@/Components/TextInput.vue";
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import { Head, Link, useForm } from "@inertiajs/vue3";
import { ref } from "vue";

defineProps({
    games: {},
});

const showForm = ref(false);

const form = useForm({
    name: "",
    platform: "",
    genre: "",
    release: "",
});

const addGame = () => {
    form.post(route("game.store"), {
        onFinish: () => {
            form.name = "";
            form.platform = "";
            form.genre = "";
            form.release = "";
        },
    });
};

const removeGame = (id) => {
    if (!confirm("Please, confirm to delete.")) return;
    useForm({}).delete(route("game.destroy", id), {
        onFinish: () => {
            alert("Success! Game Created.");
        },
    });
};
</script>

<template>
    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Dashboard
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 text-gray-900">My Games</div>

                    <button
                        class="w-full bg-green-200 p-2 font-bold my-2 border-2 border-green-200 hover:bg-green-300 rounded"
                        @click="showForm = !showForm"
                        v-if="!showForm"
                    >
                        Add new Game
                    </button>

                    <form
                        v-if="showForm"
                        @submit.prevent="addGame"
                        class="p-2 m-2"
                    >
                        <div class="justify-between items-center">
                            <label>Name</label>
                            <TextInput
                                class="block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                                v-model="form.name"
                            />

                            <label>Platform</label>
                            <TextInput
                                class="block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                                v-model="form.platform"
                            />

                            <label>Genre</label>
                            <TextInput
                                class="block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                                v-model="form.genre"
                            />

                            <label>Release</label>
                            <p class="text-xs text-gray-500">Ex: yyyy-mm-dd</p>
                            <TextInput
                                class="block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                                v-model="form.release"
                            />
                        </div>
                        <PrimaryButton
                            class="bg-white-900"
                            @click="showForm = !showForm"
                            type="button"
                            >Close</PrimaryButton
                        >
                        <SecondaryButton class="m-2" type="submit"
                            >Save</SecondaryButton
                        >
                        <!--  <div
                            @click="showForm = !showForm"
                            class="cursor-pointer font-bold block w-full text-right"
                        >
                            Close
                        </div> -->
                    </form>

                    <table
                        class="w-full table text-gray-400 border-separate space-y-6 text-sm p-2"
                    >
                        <thead class="bg-blue-200 text-gray-900">
                            <tr>
                                <th class="p-3 text-left">Name</th>
                                <th class="p-3 text-left">Platform</th>
                                <th class="p-3 text-left">Release</th>
                                <th class="p-3 text-left">Genre</th>
                                <th class="p-3 text-left">Action</th>
                            </tr>
                        </thead>
                        <tr
                            class="bg-gray-100 text-gray-900"
                            v-for="game of games"
                            :key="game.id"
                        >
                            <td class="p-3 font-semibold">{{ game.name }}</td>
                            <td class="p-3">
                                {{ game.platform }}
                            </td>
                            <td class="p-3">{{ game.release }}</td>
                            <td class="p-3">
                                <span
                                    class="inline-flex items-center gap-1 rounded-full bg-blue-100 px-2 py-1 font-semibold text-blue-900"
                                    >{{ game.genre }}</span
                                >
                            </td>
                            <td class="p-3">
                                <button
                                    class="mx-1 inline-block px-3 py-1 border-2 border-red-600 text-red-600 leading-tight rounded hover:bg-black hover:bg-opacity-5 focus:outline-none focus:ring-0 transition duration-150 ease-in-out"
                                    @click="removeGame(game.id)"
                                >
                                    Delete
                                </button>
                                <Link
                                    class="mx-1 inline-block px-3 py-1 border-2 border-purple-600 text-purple-600 leading-tight rounded hover:bg-black hover:bg-opacity-5 focus:outline-none focus:ring-0 transition duration-150 ease-in-out"
                                    :href="route('game.edit', game.id)"
                                    >Edit</Link
                                >
                            </td>
                        </tr>
                    </table>

                    <!-- <table>
                        <tr>
                            <th>Name</th>
                            <th>Platform</th>
                            <th>Genre</th>
                            <th>Release</th>
                        </tr>
                        <tr v-for="game of games" :key="game.id">
                            <td>{{ game.name }}</td>
                            <td>{{ game.platform }}</td>
                            <td>{{ game.genre }}</td>
                            <td>{{ game.release }}</td>
                            <td>
                                <button @click="removeGame(game.id)">
                                    Remove
                                </button>
                                <Link :href="route('game.edit', game.id)"
                                    >Edit</Link
                                >
                            </td>
                        </tr>
                    </table> -->
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
