<template>
  <div id="app">
    <div class="block">
      <img ref="img" src="./assets/logo.png" />
    </div>
  </div>
</template>

<script>
export default {
  name: "App",

  methods: {
    moveImg() {
      const img = this.$refs.img;

      img.onmousedown = e => {
        let coords = getCoords(img);
        let shiftX = e.pageX - coords.left;
        let shiftY = e.pageY - coords.top;

        img.style.position = "absolute";
        document.querySelector(".block").appendChild(img);
        moveAt(e);

        img.style.zIndex = 10000;

        function moveAt(e) {
          img.style.left = `${e.pageX - shiftX}px`;
          img.style.top = `${e.pageY - shiftY}px`;
        }

        document.onmousemove = e => {
          moveAt(e);
        };

        img.onmouseup = () => {
          document.onmousemove = null;
          img.onmouseup = null;
        };

        img.ondragstart = () => false;

        function getCoords(elem) {
          let box = elem.getBoundingClientRect();
          console.log(box)

          return {
            top: box.top + pageYOffset,
            left: box.left + pageXOffset
          };
        }
      };
    }
  },

  mounted() {
    this.moveImg();
  }
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
}
.block {
  width: 100vw;
  height: 100vh;
}
</style>