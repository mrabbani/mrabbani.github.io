<template>
    <div>
        <vue-typeahead v-model="value"
                       prefetch = "https://twitter.github.io/typeahead.js/data/nfl.json"
                       :default-suggestion = "false"
                       display-key = 'team'
                       :suggestion-template="myTemplate"
                       v-on:selected="done"></vue-typeahead>
        <vue-typeahead
                       prefetch = "https://twitter.github.io/typeahead.js/data/films/post_1960.json"
                       :default-suggestion = "true"
                       display-key = 'value'
                       remote = "https://twitter.github.io/typeahead.js/data/films/queries/%QUERY.json'"
                       v-on:selected="done"></vue-typeahead>
    </div>

</template>
<script>
    export default {
        data: function() {
            return{
                label:'',
                value: '',
                value1: '',
                myTemplate: '<div><h3>{{team}}</h3>'
            }
        },
        methods: {
            done: function(data) {
                console.log(data);
            }
        }
    }
</script>