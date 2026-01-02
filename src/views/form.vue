<script setup>
import { reactive, onMounted } from 'vue';
import storageService  from '@/services/StorageService';
import { useRoute, useRouter } from 'vue-router';

const router= useRouter();
const route = useRoute(); //라우터 객체 주소값 얻기

const state = reactive({
    memo: {        
        title: '',
        content: ''
    }
});
const submit = () => {
    storageService.addItem(state.memo);
    alert('저장하였습니다.');
    //라우팅 처리 (path: '/')로 주소값 이동 (화면 전환)
    router.push({
        path: '/'
    });
}

onMounted(()=> {
    if(route.params.id) {
        const id = Number(route.params.id);
        state.memo = storageService.getItem(id);
    }
});

const update = () => {
    if (!route.params.id) return;
    if (confirm("수정된 내용을 저장할까요?")) {
    const id = Number(route.params.id);
    storageService.updateItem(id, state.memo);
    alert("수정되었습니다.");
    router.push({ path: '/' });
    }
};
</script>

<template>
<form class="detail" @submit.prevent="submit">
    <div class="mb-3">
        <label for="title" class="form-label">제목</label>
        <input type="text" id="title" class="form-control p-3" v-model="state.memo.title">
    </div>
    <div class="mb-3">
        <label for="content" class="form-label">내용</label>
        <textarea id="content" v-model="state.memo.content"></textarea>
    </div>
    <button type= "submit" class="btn btn-primary w-50 py-3">저장</button>
    <button type="button" class="btn btn-outline-secondary w-50 py-3"   @click="update">수정</button>
</form>
</template>

<style scoped>

</style>