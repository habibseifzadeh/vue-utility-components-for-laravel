<template>
        <input
            :id="'moneyInput' + id"
            type="text"
            inputmode="numeric"
            @keyup="valueChanged"
            :value="initialValue">
</template>

<script>
    export default {
        name: "HabibMoneyInputComponent",
        props: [
            'initialValue', 'id'
        ],
        methods: {
            valueChanged() {
                let moneyInput = document.getElementById('moneyInput' + this.id).value;
                let onlyNumbers = moneyInput.replace(/[^0-9]/g, '');
                let onlyNumbersArr = onlyNumbers.split('');
                for(let i = onlyNumbersArr.length - 3; i > 0; i-=3) {
                    onlyNumbersArr.splice(i, 0, ',');
                }
                document.getElementById('moneyInput' + this.id).value = onlyNumbersArr.join('');
                this.$emit('value-changed', onlyNumbers);
            }
        },
        mounted() {
            this.valueChanged();
        }
    }
</script>

<style lang="scss" scoped>
</style>
