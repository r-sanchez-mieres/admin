
<template>
  <div>
    <title-bar :title-stack="titleStack" />
    <hero-bar>
      Menu
      <router-link
        slot="right"
        to="/"
        class="button"
      >
        Dashboard
      </router-link>
    </hero-bar>
    <section class="section is-main-section">
      <tiles-block>
        <card-component
          title="Menu"
          icon="menu"
          class="tile is-child"
        >
          <tree-item
            v-if="false"
            :item="treeData"
            @make-folder="makeFolder"
            @add-item="addItem"
          />

          <span>
            {{ items }}
          </span>

          <ul>
            <item
              v-for="(el) in items"
              :key="el.id || Math.random()"
              :element="el"
            />
          </ul>
        </card-component>
      </tiles-block>
    </section>
  </div>
</template>

<script>
/* eslint-disable */
import { defineComponent, Vue } from 'vue'
import { mapState } from 'vuex'
import CardComponent from '@/components/CardComponent.vue'
import TitleBar from '@/components/TitleBar.vue'
import HeroBar from '@/components/HeroBar.vue'
import TilesBlock from '@/components/TilesBlock.vue'
import TreeItem from '@/components/TreeItem.vue'
import Item from '@/components/Item.vue'

export default defineComponent({
  name: 'MenuView',
  components: {
    TilesBlock,
    HeroBar,
    TitleBar,
    CardComponent,
    'tree-item': TreeItem,
    Item
  },
  data () {
    return {
      titleStack: ['Admin', 'Menu'],
      treeData: {
        name: 'My Tree',
        children: [
          { name: 'hello' },
          { name: 'wat' },
          {
            name: 'child folder',
            children: [
              {
                name: 'child folder',
                children: [{ name: 'hello' }, { name: 'wat' }]
              },
              { name: 'hello' },
              { name: 'wat' },
              {
                name: 'child folder',
                children: [{ name: 'hello' }, { name: 'wat' }]
              }
            ]
          }
        ]
      },
      items: [
                'General',
                [
                    {
                        'id': 14,
                        'parent_id': 11,
                        'section': null,
                        'label': 'Dashboard',
                        'to': '/',
                        'href': null,
                        'icon': 'desktop-mac',
                        'sub_label': null,
                        'target': null,
                        'updateMark': false,
                        'menu': null
                    }
                ],
                'Examples',
                [
                    {
                        'id': 15,
                        'parent_id': 12,
                        'section': null,
                        'label': 'Tables',
                        'to': '/tables',
                        'href': null,
                        'icon': 'table',
                        'sub_label': null,
                        'target': null,
                        'updateMark': true,
                        'menu': null
                    },
                    {
                        'id': 16,
                        'parent_id': 12,
                        'section': null,
                        'label': 'Forms',
                        'to': '/forms',
                        'href': null,
                        'icon': 'square-edit-outline',
                        'sub_label': null,
                        'target': null,
                        'updateMark': false,
                        'menu': null
                    },
                    {
                        'id': 17,
                        'parent_id': 12,
                        'section': null,
                        'label': 'Profile',
                        'to': '/profile',
                        'href': null,
                        'icon': 'account-circle',
                        'sub_label': null,
                        'target': null,
                        'updateMark': false,
                        'menu': null
                    },
                    {
                        'id': 18,
                        'parent_id': 12,
                        'section': null,
                        'label': 'Login',
                        'to': '/login',
                        'href': null,
                        'icon': 'lock',
                        'sub_label': null,
                        'target': null,
                        'updateMark': false,
                        'menu': null
                    },
                    {
                        'id': 19,
                        'parent_id': 12,
                        'section': null,
                        'label': 'Submenus',
                        'to': null,
                        'href': null,
                        'icon': 'view-list',
                        'sub_label': null,
                        'target': null,
                        'updateMark': false,
                        'menu': [
                            {
                                'id': 20,
                                'parent_id': 19,
                                'section': null,
                                'label': 'Sub Item 1',
                                'to': null,
                                'href': '#void',
                                'icon': null,
                                'sub_label': null,
                                'target': null,
                                'updateMark': false,
                                'menu': null
                            },
                            {
                                'id': 21,
                                'parent_id': 19,
                                'section': null,
                                'label': 'Sub Item 2',
                                'to': null,
                                'href': '#void',
                                'icon': null,
                                'sub_label': null,
                                'target': null,
                                'updateMark': false,
                                'menu': null
                            }
                        ]
                    }
                ],
                'About',
                [
                    {
                        'id': 23,
                        'parent_id': 22,
                        'section': null,
                        'label': 'Premium',
                        'to': null,
                        'href': 'https://justboil.me/bulma-admin-template/one/',
                        'icon': 'monitor',
                        'sub_label': null,
                        'target': '_blank',
                        'updateMark': false,
                        'menu': null
                    },
                    {
                        'id': 24,
                        'parent_id': 22,
                        'section': null,
                        'label': 'Git Hub',
                        'to': null,
                        'href': 'https://github.com/vikdiesel/admin-one-vue-bulma-dashboard',
                        'icon': 'github-circle',
                        'sub_label': null,
                        'target': '_blank',
                        'updateMark': false,
                        'menu': null
                    }
                ]
            ]
    }
  },
  computed: {
    ...mapState([
      'userName',
      'userEmail'
    ])
  },
  mounted () {
    fetch('http://bag-sys.py:8084/api/v1/menu')
      .then(response => response.json())
      .then(data => {
        // console.log(JSON.stringify(data))
        this.items = data
      }).catch(error => {
        console.error('Error al obtener los datos:', error)
      })
  },
  methods: {
    makeFolder: function (item) {
      Vue.set(item, 'children', [])
      this.addItem(item)
    },
    addItem: function (item) {
      item.children.push({
        name: 'new stuff'
      })
    }
  }
})
</script>
