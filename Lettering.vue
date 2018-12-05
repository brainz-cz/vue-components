<script>
export default {
	data: function() {
		return {

		}
	},
	render: function(createElement) {

		var html = this.$slots.default[0].text.toString(),
			text = [],
			words = [],
			newHtml = '';

		text = html.trim().split(' ');

		text.forEach((e) => {
			words.push('<span class="lettering__letter">' + e.split('').join('</span><span class="lettering__letter">') + '</span>')
		})

		newHtml = '<span class="lettering__word">' + words.join('</span> <span class="lettering__word">') + '</span> ';

		return createElement(
			'span', {
				class: 'lettering',
				domProps: {
					innerHTML: newHtml
				}
			}
		)
	},
	mounted() {
        this.$el.classList.add('is-animating')
	}
}
</script>

<style lang="scss">

.lettering__word {
    display: inline-block;
    margin-bottom: -7px;
    margin-top: -7px;
    padding-bottom: 5px;
    padding-top: 5px;
    overflow: hidden;
    white-space: nowrap;
}

.lettering__letter {
    display: inline-block;
    transition: all 250ms cubic-bezier(0.175, 0.885, 0.32, 1.275);
    transform: translateY(-111%);

    $letterDelay: 20ms;
    @for $i from 1 to 10 {
        &:nth-child(#{$i}) {
            transition-delay: $letterDelay * $i;
        }
    }
}

.is-animating {

    .lettering__letter {
        transform: translateY(0);

        $letterDelay: 20ms;
        @for $i from 1 to 10 {
            &:nth-child(#{$i}) {
                transition-delay: $letterDelay * $i + 200;
            }
        }
    }
}
</style>
