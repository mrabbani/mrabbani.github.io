
<template>
  <input v-model="query" ref="input" class="typeahead-suggestions"
         :class="classes"
         :id = "id"
         v-bind:value="value"
         v-on:input="updateValue($event.target.value)"
         v-on:blur="formatValue"
          >
</template>
<script>
  var Bloodhound = require('typeahead.js')
  export default {
    data: function() {
      var id =  'typeahead-suggestion' + parseInt( Math.random() *100000);
      return {
        id,
        defaultSuggestions: [],
        query: ''
      };
    },

    props: {
      value: {
        type: String,
        default: ''
      },
      classes: {
        type: String,
        default: ''
      },
      displayKey: {
        type: String,
        required: true
      },
      suggestionTemplate: {
        type: String,
        default: ''
      },
      name: {
        type: String,
        default: 'Vue Auto Complete'
      },
      prefetch: {
        type: String,
        default: ''
      },
      defaultSuggestion: {
        type: Boolean,
        default: true
      },
      remote: {
        type: String,
        default: ''
      }
    },
    mounted: function() {
      var self =  this;
      var bloodhoundConfig = {};
      if(this.defaultSuggestion && this.prefetch) {
        bloodhoundConfig = {
          prefetch: {
            cache: false,
            url: self.prefetch,
            transform: function (response) {
              self.defaultSuggestions = response.splice(0, 5);
              return response;
            }
          }
        };
      } else if(this.prefetch) {
        bloodhoundConfig =  {prefetch: self.prefetch};
        }

    if(this.remote) {
      bloodhoundConfig = {
        remote: {
          url: self.remote,
          wildcard: '%QUERY'
        },
        ...bloodhoundConfig
      }
    }
    var nflTeams = new Bloodhound({
        datumTokenizer: Bloodhound.tokenizers.obj.whitespace(self.displayKey),
        queryTokenizer: Bloodhound.tokenizers.whitespace,
        identify: function(obj) { return obj[self.displayKey];},
        ...bloodhoundConfig
      });

      function nflTeamsWithDefaults(q, sync) {
        var data = nflTeams;
        if (q === '') {
          console.log(self.defaultSuggestions);
          sync(self.defaultSuggestions);
        } else {
          nflTeams.search(q, sync);
        }
      }

      var template = {};
      if(this.suggestionTemplate) {
        template = {
          templates: {
            suggestion: self.parseTemplate
          }
        }
      };

      $(document).find('#' + self.id).typeahead({
          minLength: 0,
          highlight: true
        },
        {
          name: 'nfl-teams',
          display: self.displayKey,
          source: nflTeamsWithDefaults,
          ...template
        }).on('typeahead:select', function(event, suggession) {
          self.$emit('selected', suggession);
      });
    },
    methods: {
      updateValue: function (value) {
        this.$emit('input', value)
      },
      formatValue: function () {
        this.$refs.input.value = this.value;
      },
      parseTemplate: function(data) {
        var res = Vue.compile(this.suggestionTemplate);
        var vm =new Vue({
            data,
            render: res.render,
            staticRenderFns: res.staticRenderFns
        }).$mount();

        return vm.$el;
      }
    }
  }
</script>