<template>
  <div id="app" :class="{focus: focused}">
    <header id="title-bar" class="toolbar toolbar-header draggable">
      <div class="btn-group traffic-lights">
        <button class="traffic-light traffic-light-close" @click="close"/>
        <button class="traffic-light traffic-light-minimize" @click="minimize"/>
        <button class="traffic-light traffic-light-maximize" @click="maximize"/>
      </div>
      <h1 class="title">Electron Study</h1>
      <div class="toolbar-actions">
        <div class="btn-group">
          <router-link to="/" tag="button" class="btn btn-default"><span class="icon icon-home"/></router-link>
          <router-link to="/about" tag="button" class="btn btn-default"><span class="icon icon-help"/></router-link>
        </div>
      </div>
    </header>
    <div class="window-content">
      <router-view/>
    </div>
  </div>
</template>

<script>
import { remote } from 'electron'

const { app } = remote

export default {
  name: 'App',
  data () {
    let currentWindow = remote.getCurrentWindow()
    return {
      focused: currentWindow.isFocused()
    }
  },
  methods: {
    close () {
      remote.getCurrentWindow().close()
    },
    minimize () {
      remote.getCurrentWindow().minimize()
    },
    maximize () {
      let currentWindow = remote.getCurrentWindow()
      if (currentWindow.isMaximized()) {
        currentWindow.restore()
      } else {
        currentWindow.maximize()
      }
    },
    onFocus () {
      this.focused = true
    },
    onBlur () {
      this.focused = false
    }
  },
  mounted () {
    app.on('browser-window-blur', this.onBlur)
    app.on('browser-window-focus', this.onFocus)
  },
  beforeDestroy () {
    app.removeListener('browser-window-blur', this.onBlur)
    app.removeListener('browser-window-focus', this.onFocus)
  }
}
</script>

<style lang="stylus">
#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  position relative

.traffic-lights
  float left
</style>
