<template>
    <div>
        <input
            id="money-input"
            type="text"
            inputmode="numeric"
            @keyup="valueChanged"
            :value="initialValue">
    </div>
</template>

<script>
    export default {
        name: "HabibMoneyInputComponent",
        props: [
            'initialValue'
        ],
        methods: {
            valueChanged() {
                let moneyInput = document.getElementById('money-input').value;
                let onlyNumbers = moneyInput.replace(/[^0-9]/g, '');
                let onlyNumbersArr = onlyNumbers.split('');
                for(let i = onlyNumbersArr.length - 3; i > 0; i-=3) {
                    onlyNumbersArr.splice(i, 0, ',');
                }
                document.getElementById('money-input').value = onlyNumbersArr.join('');
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
