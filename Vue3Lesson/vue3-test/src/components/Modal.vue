<template>
    <teleport to="#modal">
        <div class="modal">
            挂载到指定节点
        </div>
    </teleport>

</template>

<script lang="ts">
export default {
    name: "Modal"
}
</script>

<style scoped>
.modal {
    width: 100px;
    height: 100px;
    background-color: salmon;
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
</style>
