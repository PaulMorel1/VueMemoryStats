# VueMemoryStats

This is a Vue.js wrapper for memory-stats.js by Paul Irish. See https://github.com/paulirish/memory-stats.js
  
You must open chrome using the command line with the options "--enable-precise-memory-info".
On Windows I do this with a .bat file with the following line:

```
start chrome --enable-precise-memory-info
```

## Example Usage

```
<template>
  <VueMemoryStats corner="msBottomRight" />
</template>
<script>
import VueMemoryStats from './VueMemoryStats.vue'

export default {
  name: 'App',
  components: {
    VueMemoryStats
  }
}
</script>
```
