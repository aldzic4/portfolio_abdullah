<template>
    <Head title="Edit Project" />

<AuthenticatedLayout>
<template #header>
    <h2 class="font-semibold text-xl text-gray-800 leading-tight">Edit Project</h2>
</template>

<div class="py-12">
    <div class="max-w-4xl mx-auto sm:px-6 lg:px-8 bg-white">
        <form class="p-4" @submit.prevent="submit">
                    <div>
                        <InputLabel for="name" value="Name" />

                        <TextInput id="name" type="text" class="mt-1 block w-full" v-model="form.name" autofocus
                            autocomplete="name" />

                        <InputError class="mt-2" :message="form.errors.name" />
                    </div>
                    <div>
                        <InputLabel for="description" value="Description" />

                        <TextInput id="description" type="text" class="mt-1 block w-full" v-model="form.description" 
                            />

                        <InputError class="mt-2" :message="form.errors.description" />
                    </div>
                    <div class="mt-2">
                        <InputLabel for="image" value="Image" />

                        <TextInput id="image" type="file" class="mt-1 block w-full"
                            @input="form.image = $event.target.files[0]" />

                        <InputError class="mt-2" :message="form.errors.image" />
                    </div>
          
                    <div class="mt-2">
                        <InputLabel for="project_url" value="URL" />

                        <TextInput id="project_url" type="text" class="mt-1 block w-full" v-model="form.project_url" />

                        <InputError class="mt-2" :message="form.errors.project_url" />
                    </div>
                    <div class="mt-2">
                        <InputLabel for="skills" value="Skills" />
                        <select v-model="form.skill_id" id="skill_id" name="skill_id"
                            class="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md">
                            <option v-for="skill in skills" :key="skill.id" :value="skill.id">
                                {{ skill.name }}
                            </option>
                        </select>

                        <InputError class="mt-2" :message="form.errors.image" />
                    </div>

                    <div class="flex items-center justify-end mt-4">

                        <PrimaryButton class="ms-4" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                            Update
                        </PrimaryButton>
                    </div>
                </form>
    </div>
</div>
</AuthenticatedLayout>
</template>

<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
// import { Inertia } from '@inertiajs/inertia';

const props = defineProps({
    project: Object,
    skills: Array
})

console.log(props.project)
const form = useForm({
    _method: 'PUT',
    name: props.project?.name,
    image: null,
    project_url: props.project?.project_url,
    skill_id: props.project?.skill_id,
    description: props.project?.description
});

const submit = () => {
    form.post(route('projects.update', props.project.id))
};
</script>

