<script setup>
    defineProps({
        title : {
            type: String,
            required: true
        },
        msg: {
            type: String,
            required: false
        }
    });

    
</script>

<template>
    <div class="bg-[#f0f0f0] p-2 rounded-lg drop-shadow-xl flex items-center my-2">
        <div class="border-2 border-[#532683] rounded-lg my-1 w-[100%]">
            <p class="text-xl font-semibold">{{ title }}</p>
            <p class="text-lg">{{ msg }}</p>
        </div>
        <div class="ml-5">
            
            <button class="bg-green-500 rounded-xl" @click="$emit('promote')">
                <img src="../assets/check-square-svgrepo-com.svg" alt="" class="w-8">
            </button>
            
            <button class="bg-red-500 rounded-xl" @click="$emit('delete')">
                
                <img src="../assets/x-square-svgrepo-com.svg" alt="" class="w-8">
            </button>
            
        </div>
    </div>
</template>
