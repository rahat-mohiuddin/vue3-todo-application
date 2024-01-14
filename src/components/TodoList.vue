<script setup>
import { ref, reactive } from 'vue';

const taskList = reactive([
    {name: `Add another component to Tailwind Components`, time: 50},
    {name: `Create a Tailwind Modal Components`, time: 20},
])

const newTaskName = ref('')
const newTaskTime = ref('')

const OpenModal = ref(false);
const toggleModal = () => {
    OpenModal.value = !OpenModal.value
}
function addNewTask(){
    if(newTaskName.value.trim() !== ''){
        taskList.push({name: newTaskName.value, time: newTaskTime.value})
        newTaskName.value = ''
        newTaskTime.value = ''
    }
}

function removeTask(index){
    this.taskList.splice(index, 1)
}

</script>
<template>
    <div class="h-100 w-full flex items-center justify-center bg-teal-lightest font-sans mt-20">
        <div class="bg-white rounded shadow p-6 m-4 w-full lg:w-3/4 lg:max-w-lg">
            <div class="mb-4 flex justify-between items-center border-b pb-4">
                <div>
                    <h1 class="text-grey-darkest font-bold">Todo List</h1>
                    <small class="text-gray-600"><span class="font-semibold">N.B: </span>Complete Task in Time</small>
                </div>
                <button @click="toggleModal" class="flex-no-shrink p-2 rounded bg-blue-500 hover:bg-blue-600 text-white">Add New Task</button>
            </div>
            <div>
                <div v-for="(task, index) in taskList" :key="index" class="flex mb-4 items-center">
                    <div class="w-full">
                        <p class="w-full text-grey-darkest text-left">{{ task.name }}</p>
                        <small class="block text-gray-700">Complete the Task Within <span class="font-semibold">{{ task.time }}</span> Minute</small>
                    </div>
                    <button @click="removeTask(index)" class="flex-no-shrink p-2 ml-2 rounded bg-red-500 hover:bg-red-600 text-white hover:text-white">Remove</button>
                </div>
            </div>
        </div>
    </div>
    <transition name="modalTransition">
        <div v-show="OpenModal" class="relative z-10" aria-labelledby="modal-title" role="dialog" aria-modal="true">
            <!--
            Background backdrop, show/hide based on modal state.

            Entering: "ease-out duration-300"
            From: "opacity-0"
            To: "opacity-100"
            Leaving: "ease-in duration-200"
            From: "opacity-100"
            To: "opacity-0"
        -->
            <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"></div>

            <div class="fixed inset-0 z-10 w-screen overflow-y-auto">
                <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
                    <!--
                Modal panel, show/hide based on modal state.

                Entering: "ease-out duration-300"
                From: "opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
                To: "opacity-100 translate-y-0 sm:scale-100"
                Leaving: "ease-in duration-200"
                From: "opacity-100 translate-y-0 sm:scale-100"
                To: "opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
            -->
                    <div class="relative transform overflow-hidden rounded-lg bg-white text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg">
                        <form @submit.prevent="addNewTask">
                            <div class="bg-white px-4 pb-4 pt-5 sm:p-6 sm:pb-4">
                                <div class="sm:flex sm:items-start">
                                    <div class="mx-auto flex h-12 w-12 flex-shrink-0 items-center justify-center rounded-full bg-red-100 sm:mx-0 sm:h-10 sm:w-10">
                                        <svg class="h-6 w-6 text-red-600" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true">
                                            <path stroke-linecap="round" stroke-linejoin="round" d="M12 9v3.75m-9.303 3.376c-.866 1.5.217 3.374 1.948 3.374h14.71c1.73 0 2.813-1.874 1.948-3.374L13.949 3.378c-.866-1.5-3.032-1.5-3.898 0L2.697 16.126zM12 15.75h.007v.008H12v-.008z" />
                                        </svg>
                                    </div>
                                    <div class="mt-3 text-center sm:ml-4 sm:mt-0 sm:text-left">
                                        <h3 class="text-base font-semibold leading-6 text-gray-900" id="modal-title">Assign New Task</h3>
                                    </div>
                                </div>
                                <div class="mt-2">
                                    <label for="taskName" class="block text-sm font-medium leading-6 text-gray-900">Task Name</label>
                                    <div class="relative mt-2 rounded-md shadow-sm">
                                        <input v-model="newTaskName" type="text" name="taskName" id="taskName" class="block w-full rounded-md border-0 py-1.5 pl-3 pr-20 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:outline-none sm:text-sm sm:leading-6" placeholder="Ex: Create a Todo List">
                                    </div>
                                </div>
                                <div class="mt-2">
                                    <label for="time" class="block text-sm font-medium leading-6 text-gray-900">Time (in Minutes)</label>
                                    <div class="relative mt-2 rounded-md shadow-sm">
                                        <input v-model="newTaskTime" type="number" name="time" id="time" class="block w-full rounded-md border-0 py-1.5 px-3 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:outline-none sm:text-sm sm:leading-6" placeholder="Ex: 30 Minutes">
                                    </div>
                                </div>
                            </div>
                            <div class="bg-gray-50 px-4 py-3 sm:flex sm:flex-row-reverse sm:px-6">
                                <button @click="toggleModal" type="submit" class="inline-flex w-full justify-center rounded-md bg-green-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-green-500 sm:ml-3 sm:w-auto">Assign Task</button>
                                <button @click="toggleModal" type="button" class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:mt-0 sm:w-auto">Cancel</button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </transition>
</template>