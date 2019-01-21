<template>
    <div class="reveal">
        <img v-bind:src="src" v-bind:alt="alt">
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

		}
    },
    mounted(){
        this.onScroll();
    },
    methods: {
        onScroll: function () {
            window.addEventListener("scroll", () => {
                this.handleScroll()
            });
        },
        handleScroll: function () {
            if(this.isElementInViewport()) {
                this.reveal();
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
        reveal: function () {
            this.$el.classList.add('is-revealing');
        }
    }
}
</script>

<style lang="scss">

    .reveal {
        position: relative;
        overflow: hidden;
        z-index: -1;

        &:before {
            position: absolute;
            content: '';
            width: 200%;
            height: 200%;
            background-color: #fff;
            opacity: 1;
            transition: all 2s ease;
            transform: translate3d(-20%, -30%, 0) rotate(33deg);
        }

        &.is-revealing {
            z-index: 1;
            &:before {
                transform: translate3d(50%, 70%, 0) rotate(33deg);
            }
        }
    }

</style>
