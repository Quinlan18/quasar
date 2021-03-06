<template lang="pug">
  #theme-picker
    .row.items-stretch
      .column.q-gutter-md
        q-btn(
          v-for="color in list"
          :key="`picker-${color}`"
          :color="color"
          :text-color="dark[color] === true ? 'white' : 'black'"
          no-caps
          glossy
          unelevated
        )
          .text-body1.text-capitalize
            | {{ color }}
            .text-body2 {{ colors[color] }}

          q-menu(anchor="top left", self="top left")
            q-color(v-model="colors[color]")

      .col.q-pl-md
        .relative-position.fit.generic-border-radius.shadow-2.bg-white.overflow-hidden
          div(:class="`bg-primary text-${dark.primary === true ? 'white' : 'black'} shadow-2`")
            q-bar(dense, :dark="dark.primary")
              q-space
              q-icon.q-mr-xs(name="fas fa-square", size="12px", style="opacity: 0.5")
              q-icon.q-mr-xs(name="fas fa-circle", size="12px", style="opacity: 0.5")
              q-icon.q-mr-sm.rotate-90(name="fas fa-play", size="12px", style="opacity: 0.5")

            q-toolbar
              q-btn(flat, dense, round, icon="arrow_back")
              q-space
              q-btn(flat, dense, round, icon="search")
              q-btn(flat, dense, round, icon="menu")

            q-toolbar(inset)
              q-toolbar-title Quasar

          .q-px-md.q-py-lg
            .row.q-col-gutter-md
              .col-4(
                v-for="color in sideColors"
                :key="`card-${color}`"
              )
                q-card(flat, :class="`bg-${color} text-${dark[color] === true ? 'white' : 'black'}`")
                  q-card-section
                    .text-h6.row.no-wrap
                      .ellipsis.text-capitalize {{ color }}
                      q-space
                      q-icon(
                        v-if="color !== 'secondary'"
                        :name="$q.icon.type[color]"
                        size="24px"
                      )

                  q-card-section Lorem, ipsum dolor sit amet consectetur adipisicing elit.

            q-btn(
              fab
              icon="map"
              color="accent"
              :text-color="dark.accent === true ? 'white' : 'black'"
              class="absolute"
              style="bottom: 16px; right: 16px"
            )

    q-separator.q-mt-lg.q-mb-sm

    .col-12.row.items-center.justify-end.q-gutter-md
      q-btn(color="black", label="Export", @click="exportDialog = true")

    q-dialog(v-model="exportDialog")
      q-card
        q-tabs.text-teal(v-model="exportTab", align="justify")
          q-tab(name="styl", no-caps, label="quasar.variables.styl")
          q-tab(name="quasar-cli", no-caps, label="Quasar CLI")
          q-tab(name="umd", no-caps, label="UMD")
          q-tab(name="vue-cli", no-caps, label="Vue CLI")

        q-separator

        q-tab-panels(v-model="exportTab", animated)
          q-tab-panel(name="styl")
            doc-code(copy) {{ stylusExport }}

          q-tab-panel(name="quasar-cli")
            doc-code(copy) {{ quasarCliExport }}

          q-tab-panel(name="umd")
            doc-code(copy) {{ umdExport }}

          q-tab-panel(name="vue-cli")
            doc-code(copy) {{ vueCliExport }}

        q-separator

        q-card-actions(align="right")
          q-btn(color="white", text-color="teal", flat, label="Close", v-close-dialog)
</template>

<script>
import { colors } from 'quasar'
const { setBrand, luminosity } = colors

export default {
  data () {
    return {
      colors: {
        primary: '#027BE3',
        secondary: '#26A69A',
        accent: '#9C27B0',

        positive: '#21BA45',
        negative: '#C10015',
        info: '#31CCEC',
        warning: '#F2C037'
      },

      dark: {
        primary: true,
        secondary: true,
        accent: true,

        positive: true,
        negative: true,
        info: false,
        warning: false
      },

      exportDialog: false,
      exportTab: 'styl',
      list: ['primary', 'secondary', 'accent', 'positive', 'negative', 'info', 'warning'],
      sideColors: ['secondary', 'positive', 'negative', 'info', 'warning']
    }
  },

  watch: {
    'colors.primary' (val) {
      this.update('primary', val)
    },

    'colors.secondary' (val) {
      this.update('secondary', val)
    },

    'colors.accent' (val) {
      this.update('accent', val)
    },

    'colors.positive' (val) {
      this.update('positive', val)
    },

    'colors.negative' (val) {
      this.update('negative', val)
    },

    'colors.info' (val) {
      this.update('info', val)
    },

    'colors.warning' (val) {
      this.update('warning', val)
    }
  },

  computed: {
    stylusExport () {
      return `$primary   = ${this.colors.primary}\n` +
        `$secondary = ${this.colors.secondary}\n` +
        `$accent    = ${this.colors.accent}\n\n` +
        `$positive  = ${this.colors.positive}\n` +
        `$negative  = ${this.colors.negative}\n` +
        `$info      = ${this.colors.info}\n` +
        `$warning   = ${this.colors.warning}`
    },

    quasarCliExport () {
      return `// quasar.conf.js

return {
  framework: {
    config: {
      brand: {
        primary: '${this.colors.primary}',
        secondary: '${this.colors.secondary}',
        accent: '${this.colors.accent}',

        positive: '${this.colors.positive}',
        negative: '${this.colors.negative}',
        info: '${this.colors.info}',
        warning: '${this.colors.warning}'
      }
    }
  }
}`
    },

    umdExport () {
      return `// place before including Quasar UMD script
window.quasarConfig = {
  brand: {
    primary: '${this.colors.primary}',
    secondary: '${this.colors.secondary}',
    accent: '${this.colors.accent}',

    positive: '${this.colors.positive}',
    negative: '${this.colors.negative}',
    info: '${this.colors.info}',
    warning: '${this.colors.warning}'
  }
}`
    },

    vueCliExport () {
      return `// main.js
Vue.use(Quasar, {
  config: {
    brand: {
      primary: '${this.colors.primary}',
      secondary: '${this.colors.secondary}',
      accent: '${this.colors.accent}',

      positive: '${this.colors.positive}',
      negative: '${this.colors.negative}',
      info: '${this.colors.info}',
      warning: '${this.colors.warning}'
    }
  }
})`
    }
  },

  methods: {
    update (color, val) {
      setBrand(color, val, document.getElementById('theme-picker'))
      this.dark[color] = luminosity(val) <= 0.4
    }
  }
}
</script>
