<template>
    <div>
        <habib-money-input-component
            initial-value=""
            @value-changed="valueChanged">
        </habib-money-input-component>
        <label>{{moneyValue}}</label>
        <br>
        <habib-money-label-component :value="moneyValue"></habib-money-label-component>
        <habib-input-with-suggestion-component
            api-url="https://jsonplaceholder.typicode.com/users"
            @item-selected="itemSelected">

        </habib-input-with-suggestion-component>
    </div>
</template>

<script>
    import HabibMoneyInputComponent from "./HabibMoneyInputComponent";
    import HabibMoneyLabelComponent from "./HabibMoneyLabelComponent";
    import HabibInputWithSuggestionComponent from "./HabibInputWithSuggestionComponent";

    export default {
        name: "FormComponent",
        components: {
            HabibInputWithSuggestionComponent,
            HabibMoneyLabelComponent,
            HabibMoneyInputComponent
        },
        data() {
            return {
                moneyValue: ''
            }
        },
        methods: {
            valueChanged(value) {
                this.moneyValue = value;
            },
            itemSelected(value) {
                window.alert('selected item: ' + value);
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>
