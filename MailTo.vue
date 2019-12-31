<template>
  <a :href="link()">
    <slot />
    {{ $slots.default ? '' : to }}
  </a>
</template>

<script>
export default {
  name: 'MailTo',
  props: {
    to: {
      type: String,
      default: 'example@example.com'
    },
    subject: {
      type: String,
      default: ''
    },
    body: {
      type: String,
      default: ''
    },
    cc: {
      type: String || Array,
      default: '' || (() => ([]))
    }
  },
  methods: {
    link () {
      let link = `mailto:${this.to}?`

      if (this.subject) link += `subject=${this.subject}&`
      if (this.body) link += `body=${this.subject}&`
      if (typeof this.cc === 'object' && this.cc.length) link += `cc=${this.cc.join(', ')}&`
      else if (typeof this.cc === 'string' && this.cc) link += `cc=${this.cc}&`

      return link
    }
  }
}
</script>
