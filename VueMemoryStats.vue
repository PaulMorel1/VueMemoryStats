<template></template>
<script>
  /*
  This is a Vue.js wrapper for memory-stats.js by Paul Irish.
  See https://github.com/paulirish/memory-stats.js
  
  You must open chrome using the command line with the options "--enable-precise-memory-info".
  On Windows I do this with a .bat file with the following line:
  
  start chrome --enable-precise-memory-info
  
  This assumes that you have the memory stats js file in a file called "memory-stats.js".
  See https://github.com/paulirish/memory-stats.js/blob/master/memory-stats.js
  */
  import MemoryStats from './memory-stats.js';
  
  export default {
    props: {
	  corner: String // msTopLeft, msTopRight, msBottomLeft, msBottomRight
	},
    data: function () {
      return {
	    stats: new MemoryStats()
      }
    },
	mounted: function () {
	  var stats = this.stats; // Get a reference to the stats object. This is needed for the callback below, and to make the code more concise.
	  stats.domElement.classList.add(this.corner); // Add the class that describes where the memory stats widget will appear.
      document.body.appendChild( stats.domElement ); // Add the stats element to the page.

	  // Modify the requestAnimationFrame method, which runs every frame, to also update the memory stats.
      requestAnimationFrame(function rAFloop(){
        stats.update();
        requestAnimationFrame(rAFloop);
      });
	}
  }
</script>

<style>
/*
  This styles are the possible values for the "corner" property.
*/
.msTopLeft {
  position: fixed;
  left: 0px;
  top: 0px;
}
.msTopRight {
  position: fixed;
  right: 0px;
  top: 0px;
}
.msBottomLeft {
  position: fixed;
  left: 0px;
  bottom: 0px;
}
.msBottomRight {
  position: fixed;
  right: 0px;
  bottom: 0px;
}
</style>