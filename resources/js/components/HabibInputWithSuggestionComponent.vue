<template>
    <div id="input-with-suggestion">
        <input id="input" type="text" :value="searchTxt" @input="searchTxt = $event.target.value">
        <div id="dummy-for-position">
            <div id="results">
                <div :id="item.id" class="item" @click="itemSelected" v-for="item in items">{{item.name}}</div>
            </div>
        </div>
        hello
    </div>
</template>

<script>
    export default {
        name: "HabibInputWithSuggestionComponent",
        props: [
            'apiUrl', 'initialValue', 'headers'
        ],
        watch: {
            searchTxt() {
                if(this.searchTxt === '') {
                    document.getElementById('results').style.display = 'none';
                } else {
                    this.beginSearch();
                }
            }
        },
        data() {
            return {
                searchTxt: '',
                items: Array
            }
        },
        methods: {
            beginSearch: _.debounce(function () {
                let that = this;
                axios.get(that.apiUrl + that.searchTxt, {
                    headers: that.headers
                }).then(response => {
                        return response.data;
                    }
                ).then(data => {
                    if(this.searchTxt !== '') {
                        document.getElementById("results").style.display = 'block';
                        if(data.length < 1) {
                            that.items = [{id: -1, name: 'No results found'}];
                        } else {
                            that.items = data;
                        }
                    }
                })
            }, 500),
            itemSelected(event) {
                let id = event.target.getAttribute('id');
                console.log(id);
                this.$emit('item-selected', id);
                document.getElementById("results").style.display = 'none';
                document.getElementById('input').value = event.target.innerText;
            }
        },
        mounted() {
            document.getElementById('input').defaultValue = this.initialValue;
        }
    }
</script>

<style lang="scss" scoped>
    #input-with-suggestion {
        width: 50%;
        position: relative;

        input {
            width: 100%;
            padding: .5rem 0;
        }

        #dummy-for-position {
            position: absolute;
            width: 100%;
            #results {
                border: 1px solid black;
                box-shadow: 2px 2px 10px;
                margin: 0 auto;
                display: none;
                position: absolute;
                width: 100%;
                top: 0;
                left: 0;
                z-index: 100;
                background: white;

                .item {
                    cursor: pointer;
                    padding: .5rem;

                    &:hover {
                        background: lightblue;
                    }
                }
            }
        }
    }
</style>
