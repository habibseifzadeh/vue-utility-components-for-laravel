<template>
    <span>{{moneyValue}}</span>
</template>

<script>
    export default {
        name: "HabibMoneyLabelComponent",
        props: [
            'value'
        ],
        computed: {
            moneyValue() {
                if(this.value === undefined || this.value === null) {
                    return '';
                }
                let tempValue = this.value.toString();
                let onlyNumbers = this.value.replace(/[^0-9]/g, '');
                let onlyNumbersArr = onlyNumbers.split('');
                for (let i = onlyNumbersArr.length - 3; i > 0; i -= 3) {
                    onlyNumbersArr.splice(i, 0, ',');
                }
                return  onlyNumbersArr.join('');
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>
