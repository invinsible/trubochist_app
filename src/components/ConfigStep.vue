<template>
    <div class="grid">
        <p class="pic" v-for="el in pics" :key="el.id">{{el.id}}</p>
    </div>
</template>

<script>
export default {
    name: 'ConfigStep',

    data() {
        return {
            pics: [
                {
                    id: 0,
                    background: '0'
                },
                {
                    id: 1,
                    background: '1'
                },
                {
                    id: 2,
                    background: '2'
                },
                {
                    id: 3,
                    background: '3'
                },
                {
                    id: 4,
                    background: '4'
                }
            ]
        }
    }
}
</script>

<style>
.pic {
    width: 45px;
    height: 45px;
    cursor: pointer;
    transition: opacity 0.3s;
}
.pic:hover {
    opacity: .8;
}
.pic:active {
    opacity: .4;
}
</style>