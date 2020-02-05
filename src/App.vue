<template>
  <div id="app">
    <div ref="slider" class="slider">
      <img
        ref="img"
        src="./assets/wildlife-safari-animals-zookeepers-nature-forest-jungle-giraffe-funny-gift-thomas-larch-transparent.jpeg"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "App",

  mounted() {
    this.moveImg();
  },

  methods: {
    moveImg() {
      let thumb = this.$refs.img;
      let slider = this.$refs.slider;
      let thumbWidth = thumb.offsetWidth

      thumb.onmousedown = event => {
        event.preventDefault();

        let shift = event.clientX - thumb.getBoundingClientRect().left;

        document.addEventListener("mousemove", onMouseMove);
        document.addEventListener("mouseup", onMouseUp);

        function onMouseMove(event) {
          let newLeft = `${event.clientX - shift - slider.getBoundingClientRect().left}`;

          if (newLeft < - thumbWidth / 2) {
            newLeft = - thumbWidth / 2;
          }

          let rightEdge = slider.offsetWidth - thumb.offsetWidth;

          if (newLeft > rightEdge + thumbWidth / 2) {
            newLeft = rightEdge + thumbWidth / 2;
          }

          thumb.style.left = `${newLeft}px`;
        }

        function onMouseUp() {
          document.removeEventListener("mouseup", onMouseUp);
          document.removeEventListener("mousemove", onMouseMove);
        }
      };

      thumb.ondragstart = () => false;
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

.slider {
  width: 600px;
  border-radius: 5px;
  background: #e0e0e0;
  background: linear-gradient(left top, #e0e0e0, #eeeeee);
  height: 15px;
  margin: 300px auto;
}

img {
  height: 150px;
  width: 150px;
  position: relative;
  cursor: pointer;
  bottom: 75px;
  left: calc(50% - 75px);
}
</style>