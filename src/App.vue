<template>
  <div id="app">
    <header class="toolbar toolbar-header">
      <h1 class="title">Electron Study</h1>
      <div class="toolbar-actions">
        <div class="btn-group">
          <router-link to="/" tag="button" class="btn btn-default"><span class="icon icon-home" /></router-link>
          <router-link to="/about" tag="button" class="btn btn-default"><span class="icon icon-help" /></router-link>
        </div>
      </div>
    </header>
    <div class="window-content">
      <router-view/>
    </div>
  </div>
</template>

<style lang="stylus">
#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
header.toolbar
  -webkit-user-select none
  -webkit-app-region drag
</style>
