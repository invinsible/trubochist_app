<template>
    <div class="grid">
        <p>
          <label for="vulkan_rus">Нержавеющая сталь Вулкан (Россия)</label>
          <input type="radio" id="vulkan_rus" value="vulkan_rus" v-model="material" />
        </p>
        <p v-if="fuel === 'ugol' || fuel === 'drova'">
          <label for="pemza_swe">Вулканическая пемза Heda, Keddy (Швеция)</label>
          <input type="radio" id="pemza_swe" value="pemza_swe" v-model="material" />
        </p>
        <p v-if="fuel !== 'gaz' || fuel !== 'dizel'">
          <label for="hart_ger">Керамическая Hart (Германия)</label>
          <input type="radio" id="hart_ger" value="hart_ger" v-model="material" />
        </p>
    </div>
</template>

<script>
export default {
    name: 'MaterialStep',
    props: {
        fuel: String,
    },
    data() {
        return {
            material: null,
        }        
    },
    watch: {
        fuel() {
            this.material = null;
        },
        material() {
            this.$emit('choose', {step: 'material', value: this.material});
        }
    }
}
</script>