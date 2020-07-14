<template>
    <span id="money-label"></span>

</template>

<script>
    export default {
        name: "HabibMoneyLabelComponent",
        props: [
            'value'
        ],
        watch: {
            value(newVal) {
                this.setValue(newVal);
            }
        },
        methods: {
            setValue(value) {
                let onlyNumbers = value.replace(/[^0-9]/g, '');
                let onlyNumbersArr = onlyNumbers.split('');
                for (let i = onlyNumbersArr.length - 3; i > 0; i -= 3) {
                    onlyNumbersArr.splice(i, 0, ',');
                }
                document.getElementById('money-label').innerText = onlyNumbersArr.join('');
            }
        },
        mounted() {
            this.setValue(this.value);
        }
    }
</script>

<style lang="scss" scoped>

</style>
