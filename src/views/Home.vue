<script setup>
import { onMounted, reactive } from 'vue';
import { StorageService, StorageService } from '@/services/StorageService';

const storageService = new StorageService('myMemo');
//StorageService클래스 내에 있는 생성자 호출
//생성자 호출시에는 new키워드가 앞에 있어야 한다.

const state = reactive({
    memos: {}
});
onMounted( ()=> state.memos = storageService.getItems() );
</script>

<template>
    <div class="memo-list">
        <router-link class = "item" v-for="item in state.memos" :to="`/memos/${item.id}`">
            
        </router-link>
    </div>
</template>

<style scoped>

</style>