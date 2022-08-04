<script lang="ts">
export default {
    name: 'BackButton',
    props: {
        address: {
            type: String,
            default: 'https://ec2.zhuxiaotan.xyz'
        },
        pageName: {
            type: String,
            default: 'Welocome Page'
        }
    }
}
</script>

<template>
    <a :href="address">Back to {{ pageName }}</a>
</template>

<style scoped>
a {
    position: fixed;
    top: 15px;
    left: 15px;
    z-index: 1;
    color: rgb(251, 251, 253);
    font-weight: 500;
}

i {
    font-style: normal;
}
</style>