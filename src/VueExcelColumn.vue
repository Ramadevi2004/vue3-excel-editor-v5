<template>
  <div />
</template>

<script>
export default {
  props: {
    field: { type: String, default: 'dummy' },
    label: { type: String, default: null },
    type: { type: String, default: 'string' },
    initStyle: { type: [Object, Function], default: null },
    width: { type: String, default: '100px' },
    invisible: { type: Boolean, default: false },
    readonly: { type: Boolean, default: null },
    textTransform: { type: String, default: null }, // replace uppercase prop
    textAlign: { type: String, default: null },
    keyField: { type: Boolean, default: false },
    sticky: { type: Boolean, default: false },
    listByClick: { type: Boolean, default: null },

    validate: { type: Function, default: null },
    change: { type: Function, default: null },
    link: { type: Function, default: null },
    isLink: { type: Function, default: null },
    format: { type: String, default: 'text' },
    cellClick: { type: Function, default: null },
    autoFillWidth: { type: Boolean, default: false },
    hideDuplicate: { type: Boolean, default: false },
    grouping: { type: String, default: null },

    allowKeys: { type: [Array, Function], default() { return null } },
    mandatory: { type: String, default: '' },
    lengthLimit: { type: Number, default: 0 },
    autocomplete: { type: Boolean, default: null },
    pos: { type: Number, default: 0 },
    options: { type: [Array, Object, Function], default() { return null } },
    summary: { type: String, default: null },
    sort: { type: Function, default: null },
    sorting: { type: Function, default: null },
    noSorting: { type: Boolean, default: null },
    masking: { type: String, default: '•' },
    placeholder: { type: String, default: '' },
    color: { type: [String, Function], default: null },
    bgcolor: { type: [String, Function], default: null },

    // New props for multiselect
    delimiter: { type: String, default: ',' }, // Delimiter for storing multiple values
    displayDelimiter: { type: String, default: ', ' }, // Delimiter for displaying values

    toValue: {
      type: Function,
      default(text) {
        switch (this.textTransform) {
          case 'uppercase':
            text = text.toUpperCase()
            break
          case 'lowercase':
            text = text.toLowerCase()
            break
        }
        switch (this.type) {
          case 'datetick':
            return new Date(text + ' GMT+0').getTime()
          case 'datetimetick':
            return new Date(text + ' GMT+0').getTime()
          case 'datetimesectick':
            return new Date(text + ' GMT+0').getTime()
          case 'check10':
          case 'checkYN':
          case 'checkTF':
            return text.toUpperCase()
          case 'map':
            if (this.options.constructor.name.endsWith('Function')) {
              const list = this.options(text)
              return Object.keys(list).find(k => list[k] === text)
            }
            else
              return Object.keys(this.options).find(k => this.options[k] === text)
          case 'multiselect':
            // For multiselect, we keep values as is (already processed by the editor)
            return text
          default:
            return text
        }
      }
    },
    toText: {
      type: Function,
      default(val) {
        // § magic to hide the temp key
        if (this.keyField && val && val.toString().startsWith('§')) return ''
        const offset = new Date().getTimezoneOffset() * 60 * 1000
        let d
        switch (this.type) {
          case 'date':
            d = new Date(val).getTime()
            if (!d) return ''
            return new Date(d - offset).toISOString().slice(0, 10)
          case 'datetick':
            d = new Date(val * 1 ? val * 1 : val).getTime()
            if (!d) return ''
            return new Date(d - offset).toISOString().slice(0, 10)
          case 'datetimetick':
            d = new Date(val * 1 ? val * 1 : val).getTime()
            if (!d) return ''
            return new Date(d - offset).toISOString().replace('T', ' ').slice(0, 16)
          case 'datetimesectick':
            d = new Date(val * 1 ? val * 1 : val).getTime()
            if (!d) return ''
            return new Date(d - offset).toISOString().replace('T', ' ').slice(0, 19)
          case 'map':
            if (this.options.constructor.name.endsWith('Function'))
              return this.options(val)[val]
            else
              return this.options[val]
          case 'multiselect':
            if (!val) return ''
            const values = val.split(this.delimiter)

            // Handle different option formats
            if (this.options) {
              if (this.options.constructor.name.endsWith('Function')) {
                const optionMap = this.options(val)
                return values.map(v => optionMap[v] || v).join(this.displayDelimiter)
              } else if (Array.isArray(this.options)) {
                // If options is an array of {value, label} objects
                if (this.options.length > 0 && typeof this.options[0] === 'object') {
                  return values.map(v => {
                    const option = this.options.find(opt => opt.value === v)
                    return option ? option.label : v
                  }).join(this.displayDelimiter)
                }
                // If options is a simple array
                return values.join(this.displayDelimiter)
              } else {
                // If options is an object
                return values.map(v => this.options[v] || v).join(this.displayDelimiter)
              }
            }

            return values.join(this.displayDelimiter)
          case 'password':
            return this.masking.repeat(val?.length || 0)
          case 'action':
            return ''
          case 'badge':
            if (this.bgcolor) {
              let bgcolor = this.bgcolor
              if (typeof bgcolor == 'function') bgcolor = bgcolor(val)
              return `<span class='badge' style='background-color:${bgcolor}'>${val}</span>`
            }
            else
              return `<span class='badge'>${val}</span>`
          default:
            return val
        }
      }
    },
    register: { type: Function, default: null }
  },
  created() {
    this.init()
  },
  methods: {
    init() {
      const self = this
      let style = this.initStyle || {}
      let validate = this.validate
      let allowKeys = this.allowKeys
      let lengthLimit = this.lengthLimit

      switch (this.type) {
        case 'number':
          style.textAlign = 'right'
          allowKeys = allowKeys || ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '.', '-']
          break
        case 'date':
          allowKeys = allowKeys || ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '-']
          break
        case 'datetime':
          allowKeys = allowKeys || ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '-', ' ', ':']
          break
        case 'datetimesec':
          allowKeys = allowKeys || ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '-', ' ', ':']
          break
        case 'datetick':
          allowKeys = allowKeys || ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '-', ' ', ':']
          break
        case 'datetimetick':
          allowKeys = allowKeys || ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '-', ' ', ':']
          break
        case 'datetimesectick':
          allowKeys = allowKeys || ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '-', ' ', ':']
          break
        case 'check10':
          style.textAlign = 'center'
          style.textTransform = 'uppercase'
          allowKeys = allowKeys || ['0', '1']
          lengthLimit = lengthLimit || 1
          break
        case 'checkYN':
          style.textAlign = 'center'
          style.textTransform = 'uppercase'
          allowKeys = allowKeys || ['Y', 'N']
          lengthLimit = lengthLimit || 1
          break
        case 'checkTF':
          style.textAlign = 'center'
          style.textTransform = 'uppercase'
          allowKeys = allowKeys || ['T', 'F']
          lengthLimit = lengthLimit || 1
          break
        case 'map':
          this._listByClick = true 
          if (this.options.constructor.name === 'AsyncFunction')
            throw new Error('VueExcelColumn: Map does not support Async Function')
          break
        case 'select':
          this._listByClick = true 
          break
        case 'multiselect':
          // Set up multiselect specific settings
          this._listByClick = true // Ensure we can click to open dropdown
          if (this.options.constructor.name === 'AsyncFunction')
            throw new Error('VueExcelColumn: Multiselect does not support Async Function')
          break
        case 'string':
          break
        case 'password':
          break
        case 'action':
          this._listByClick = true
          break
        case 'badge':
          this._color = 'white'
          this._bgcolor = 'blue'
          this._format = 'html'
          style.textAlign = 'center'
          break
        default:
          throw new Error('VueExcelColumn: Not supported type:' + this.type)
      }

      if (this.textTransform) style.textTransform = this.textTransform
      if (this.textAlign) style.textAlign = this.textAlign

      this._autocomplete = self.autocomplete || self.type === 'action' || self.type === 'multiselect'
      this._readonly = self.readonly

      this.$parent.registerColumn({
        name: this.field,
        label: this.label === null ? this.field : this.label,
        type: this.type,
        width: this.width,
        origWidth: this.width,
        autoFillWidth: this.autoFillWidth,

        validate: validate,
        change: this.change,
        link: this.link,
        isLink: this.isLink || (this.link ? () => true : null),
        sort: this.sort,
        sorting: this.sorting,
        noSorting: this.noSorting !== null ? this.noSorting : self.$parent.noSorting,

        keyField: this.keyField,
        sticky: this.sticky,
        allowKeys: allowKeys,
        mandatory: this.mandatory,
        lengthLimit: Number(lengthLimit),
        textTransform: this.textTransform,

        get autocomplete() {
          if (self.type === 'map' || self.type === 'select' || self.type === 'multiselect') return true
          if (self.type === 'password') return false
          return self._autocomplete === null ? self.$parent.autocomplete : self._autocomplete
        },
        set autocomplete(val) {
          self._autocomplete = val
        },
        initStyle: style,
        invisible: this.invisible,
        get readonly() {
          if (self.link) return true
          if (self.type === 'action' || self.type === 'multiselect') return false
          return self._readonly === null ? self.$parent.readonly : self._readonly
        },
        set readonly(val) {
          self._readonly = val
        },
        pos: Number(this.pos),
        options: this.options,
        summary: this.summary,
        masking: this.masking,
        format: this._format || this.format,
        toValue: this.toValue,
        toText: (...arg) => {
          const result = this.toText(...arg)
          if (this.placeholder && result === '') return this.placeholder
          return result
        },
        register: this.register,
        placeholder: this.placeholder,
        cellClick: this.cellClick,
        listByClick: this.listByClick || this._listByClick,
        color: this.color || this._color,
        bgcolor: this.bgcolor || this._bgcolor,
        hideDuplicate: this.hideDuplicate || this.grouping,
        grouping: this.grouping,

        // Pass multiselect specific props
        multiselect: this.type === 'multiselect',
        delimiter: this.delimiter,
        displayDelimiter: this.displayDelimiter
      })
    }
  }
}
</script>