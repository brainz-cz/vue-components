<template>
    <div class="reveal">
      <div
        class="mask"
        :style="maskStyle"
      >
        <img
          :src="src"
          :alt="alt"
          :style="imageStyle"
          @load="loader"
        >
      </div>
    </div>
</template>


<script>
export default {
    props: {
        src: {
            type: String,
            default: '',
        },
        alt: {
            type: String,
            default: '',
        },
        threshold: {
            type: Number,
            default: 0
        }
    },
    data: function() {
      return {
        reveal: false,
        imageWidth: 'auto',
        imageHeight: 'auto'
      }
    },
    computed: {
      maskStyle() {

        var maskWidth = (50*Math.sqrt(2)*(this.imageHeight+this.imageWidth))/this.imageWidth + '%';
        var maskTransform = `rotate(-45deg) translate3d(-${(100*this.imageHeight)/(this.imageHeight+this.imageWidth)}%, -100%, 0)`;

        if(this.reveal){
          maskTransform = `rotate(-45deg) translate3d(-${(100*this.imageHeight)/(this.imageHeight+this.imageWidth)}%, 0%, 0)`;
        }

        return {
          width: maskWidth,
          paddingBottom: maskWidth,
          marginBottom: ((50*(Math.sqrt(2)*this.imageHeight-2*this.imageHeight+Math.sqrt(2)*this.imageWidth))/this.imageWidth)*-1 + '%',
          transform: maskTransform,
        }
      },
      imageStyle() {

        var imageTransform = `rotate(45deg) translate3d(${(50*(2*this.imageHeight+this.imageWidth))/this.imageWidth}%, ${(50*this.imageWidth)/this.imageHeight}%, 0)`;

        if(this.reveal){
          imageTransform = `rotate(45deg) translate3d(${this.imageHeight/this.imageWidth/2*100}%, -50%, 0)`;
        }

        return {
          width: (100*Math.sqrt(2)*this.imageWidth)/(this.imageHeight+this.imageWidth) + '%',
          transform: imageTransform,
        }
      }
    },
    mounted(){
        this.onScroll();
    },
    methods: {
        loader() {
            this.imageWidth = this.$el.querySelector('img').clientWidth;
            this.imageHeight = this.$el.querySelector('img').clientHeight;
        },
        onScroll: function () {
            window.addEventListener("scroll", () => {
                this.handleScroll()
            });
        },
        handleScroll: function () {
            if(this.isElementInViewport()) {
                this.reveal = true;
            }
        },
        isElementInViewport: function () {

            var rect = this.$el.getBoundingClientRect();

            return (
                rect.top + this.$props.threshold <= (window.innerHeight || document.documentElement.clientHeight)
            );
        },
        getElemDistance: function ( elem ) {
            var location = 0;
            if (elem.offsetParent) {
                do {
                    location += elem.offsetTop;
                    elem = elem.offsetParent;
                } while (elem);
            }
            return location >= 0 ? location : 0;
        },
    }
}
</script>

<style lang="scss">

    .reveal {
      position: relative;
      overflow: hidden;
      display: inline-block;

      .mask{
        position: relative;
        overflow: hidden;
        height: 0;
        transition: transform 1s ease-out;
        transform-origin: 0 0;
      }

      img {
        position: relative;
        transition: transform 1s ease-out;
        transform-origin: 0 0;
        height: auto;
      }
    }

</style>
