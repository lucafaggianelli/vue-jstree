<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>{{ msg }}</h1>
    <h2>Tree View</h2>
    <div>
      <div style="width:840px; margin: 0 auto;">
        <div style="width:49%; display:inline-block; vertical-align: top;">
          <v-jstree
              :data="data"
              text-field-name="title"
              show-checkbox
              multiple
              allow-batch
              whole-row
              draggable
              @item-drop="itemDrop"
              ref="tree">
            <template slot-scope="props">
              {{ props.selected }} {{ props.item.title }}
            </template>
          </v-jstree>
        </div>
        <div style="width:50%; display:inline-block;">
        <textarea style="height:300px; width:100%;">
          {{ data }}
        </textarea>
        </div>
      </div>
    </div>
    <h2>Async Loading</h2>
    <div>
      <div style="width:840px; margin: 0 auto;">
        <div style="width:49%; display:inline-block; vertical-align: top;">
          <v-jstree
              :data="asyncData"
              :async="loadData"
              show-checkbox
              multiple
              allow-batch
              whole-row>
          </v-jstree>
        </div>
        <div style="width:50%; display:inline-block; vertical-align: top;">
        <textarea style="height:300px; width:100%;">
          {{ asyncData }}
        </textarea>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'app',
    data () {
      return {
        msg: 'A Tree Plugin For Vue2',
        data: [
          {
            'title': 'Same but with checkboxes',
            'children': [
              {
                'title': 'initially selected',
                'selected': true
              },
              {
                'title': 'custom icon',
                'icon': 'fa fa-warning icon-state-danger'
              },
              {
                'title': 'initially open',
                'icon': 'fa fa-folder icon-state-default',
                'opened': true,
                'children': [
                  {
                    'title': 'Another node'
                  }
                ]
              },
              {
                'title': 'custom icon',
                'icon': 'fa fa-warning icon-state-warning'
              },
              {
                'title': 'disabled node',
                'icon': 'fa fa-check icon-state-success',
                'disabled': true
              }
            ]
          },
          {
            'title': 'Same but with checkboxes',
            'opened': true,
            'children': [
              {
                'title': 'initially selected',
                'selected': true
              },
              {
                'title': 'custom icon',
                'icon': 'fa fa-warning icon-state-danger'
              },
              {
                'title': 'initially open',
                'icon': 'fa fa-folder icon-state-default',
                'opened': true,
                'children': [
                  {
                    'title': 'Another node'
                  }
                ]
              },
              {
                'title': 'custom icon',
                'icon': 'fa fa-warning icon-state-warning'
              },
              {
                'title': 'disabled node',
                'icon': 'fa fa-check icon-state-success',
                'disabled': true
              }
            ]
          },
          {
            'title': 'And wholerow selection'
          }
        ],
        asyncData: [],
        loadData: (oriNode, resolve) => {
          console.log(oriNode)
          var id = oriNode.data.id ? oriNode.data.id : 0
          setTimeout(() => {
            let data = []
            if (id > 20) {
              data = []
            } else {
              data = [
                {
                  'text': 'New Item 1...' + id
                },
                {
                  'text': 'New Item 2...' + id
                }
              ]
            }
            resolve(data)
          }, 500)
        }
      }
    },
    methods: {
      itemDrop (node) {
        console.log('dropped', node.title)
      }
    }
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

div{
  display: block;
}
</style>
