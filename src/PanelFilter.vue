<template>
  <div id="panelModal" v-show="show" class="panel-modal" @click="clickOutside" @keydown.exact.esc="hidePanel">
    <div ref="panelFilter" class="panel-body">
      <div class="panel-title">
        <svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="sort-amount-down" role="img"
          xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"
          class="svg-inline--fa fa-sort-amount-down fa-w-16 fa-1x">
          <path fill="currentColor"
            d="M304 416h-64a16 16 0 0 0-16 16v32a16 16 0 0 0 16 16h64a16 16 0 0 0 16-16v-32a16 16 0 0 0-16-16zm-128-64h-48V48a16 16 0 0 0-16-16H80a16 16 0 0 0-16 16v304H16c-14.19 0-21.37 17.24-11.29 27.31l80 96a16 16 0 0 0 22.62 0l80-96C197.35 369.26 190.22 352 176 352zm256-192H240a16 16 0 0 0-16 16v32a16 16 0 0 0 16 16h192a16 16 0 0 0 16-16v-32a16 16 0 0 0-16-16zm-64 128H240a16 16 0 0 0-16 16v32a16 16 0 0 0 16 16h128a16 16 0 0 0 16-16v-32a16 16 0 0 0-16-16zM496 32H240a16 16 0 0 0-16 16v32a16 16 0 0 0 16 16h256a16 16 0 0 0 16-16V48a16 16 0 0 0-16-16z"
            class=""></path>
        </svg>

        <span v-html="localizedLabel.sortingAndFiltering" />
      </div>
      <div class="panel-content">
        <div class="panel-action">
          <button class="panel-button float-left" @click="sort(-1)">
            <!-- <svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="sort-amount-down" role="img"
              xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"
              class="svg-inline--fa fa-sort-amount-down fa-w-16 fa-1x">
              <path fill="currentColor"
                d="M304 416h-64a16 16 0 0 0-16 16v32a16 16 0 0 0 16 16h64a16 16 0 0 0 16-16v-32a16 16 0 0 0-16-16zm-128-64h-48V48a16 16 0 0 0-16-16H80a16 16 0 0 0-16 16v304H16c-14.19 0-21.37 17.24-11.29 27.31l80 96a16 16 0 0 0 22.62 0l80-96C197.35 369.26 190.22 352 176 352zm256-192H240a16 16 0 0 0-16 16v32a16 16 0 0 0 16 16h192a16 16 0 0 0 16-16v-32a16 16 0 0 0-16-16zm-64 128H240a16 16 0 0 0-16 16v32a16 16 0 0 0 16 16h128a16 16 0 0 0 16-16v-32a16 16 0 0 0-16-16zM496 32H240a16 16 0 0 0-16 16v32a16 16 0 0 0 16 16h256a16 16 0 0 0 16-16V48a16 16 0 0 0-16-16z"
                class=""></path>
            </svg> -->

            <span v-html="localizedLabel.sortAscending" />
          </button>
          <button class="panel-button float-right" @click="sort(1)">
            <!-- <svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="sort-alpha-up-alt" role="img"
              xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"
              class="svg-inline--fa fa-sort-alpha-up-alt fa-w-14">
              <path fill="currentColor"
                d="M16 160h48v304a16 16 0 0 0 16 16h32a16 16 0 0 0 16-16V160h48c14.21 0 21.38-17.24 11.31-27.31l-80-96a16 16 0 0 0-22.62 0l-80 96C-5.35 142.74 1.78 160 16 160zm272 64h128a16 16 0 0 0 16-16v-32a16 16 0 0 0-16-16h-56l61.26-70.45A32 32 0 0 0 432 65.63V48a16 16 0 0 0-16-16H288a16 16 0 0 0-16 16v32a16 16 0 0 0 16 16h56l-61.26 70.45A32 32 0 0 0 272 190.37V208a16 16 0 0 0 16 16zm159.06 234.62l-59.27-160A16 16 0 0 0 372.72 288h-41.44a16 16 0 0 0-15.07 10.62l-59.27 160A16 16 0 0 0 272 480h24.83a16 16 0 0 0 15.23-11.08l4.42-12.92h71l4.41 12.92A16 16 0 0 0 407.16 480H432a16 16 0 0 0 15.06-21.38zM335.61 400L352 352l16.39 48z"
                class=""></path>
            </svg> -->

            <span v-html="localizedLabel.sortDescending" />
          </button>
        </div>
        <div class="panel-action">
          <!-- <button class="panel-button float-middle" @click="freezeOrUnFreezeColumn">
<<<<<<< HEAD
            {{ isSticky ? localizedLabel.unFreezeColumn : localizedLabel.freezeColumn }}  
          </button> -->
          <button class="panel-button float-middle" @click="freezeOrUnFreezeColumn">
            <span  style="color: black;"   v-html="isSticky ? localizedLabel.unFreezeColumn : localizedLabel.freezeColumn"></span>
          </button>
=======
    {{ isSticky ? "UnFreeze Column" : localizedLabel.freezeColumn }}  
  </button> -->
        <button class="panel-button float-middle" @click="freezeOrUnFreezeColumn">
            <span  v-html="isSticky ? localizedLabel.unFreezeColumn : localizedLabel.freezeColumn"></span>
        </button>

>>>>>>> 76eee5c (fixed filter issues)
        </div>
        <div class="panel-action">
          <div>
            <button class="panel-input-button" @click="showDropdown = !showDropdown">{{ symbol }}</button>
            <div :class="{ show: showDropdown }" class="panel-dropdown">
              <div class="panel-dropdown-item" @click.prevent="setFilterCondition('')"><span
                  v-html="localizedLabel.near" /></div>
              <div class="panel-dropdown-item" @click.prevent="setFilterCondition('=')"><span
                  v-html="localizedLabel.exactMatch" /></div>
              <div class="panel-dropdown-item" @click.prevent="setFilterCondition('<>')"><span
                  v-html="localizedLabel.notMatch" /></div>
              <div class="panel-dropdown-item" @click.prevent="setFilterCondition('>')"><span
                  v-html="localizedLabel.greaterThan" /></div>
              <div class="panel-dropdown-item" @click.prevent="setFilterCondition('>=')"><span
                  v-html="localizedLabel.greaterThanOrEqualTo" /></div>
              <div class="panel-dropdown-item" @click.prevent="setFilterCondition('<')"><span
                  v-html="localizedLabel.lessThan" /></div>
              <div class="panel-dropdown-item" @click.prevent="setFilterCondition('<=')"><span
                  v-html="localizedLabel.lessThanOrEqualTo" /></div>
              <div class="panel-dropdown-item" @click.prevent="setFilterCondition('~')"><span
                  v-html="localizedLabel.regularExpression" /></div>
            </div>
            <span class="panel-input-b">
              <!-- <input type="text" ref="inputFilter" class="panel-input" :placeholder="localizedLabel.customFilter"
                :disabled="selectedItems.length > 0" trim autocomplete="off" autocorrect="off" autocapitalize="off"
                spellcheck="false" @keyup="doInputFilter" @keydown.exact.enter="doFilter"  /> -->
                <input 
                  type="text" 
                  ref="inputFilter" 
                  class="panel-input" 
                  :placeholder="localizedLabel.customFilter"
                  :disabled="!this.sortedUniqueValueList.length"
                  trim 
                  autocomplete="off" 
                  autocorrect="off" 
                  autocapitalize="off"
                  spellcheck="false" 
                  @keyup="doInputFilter" 
                  @keydown.exact.enter="doFilter" 
                />
            </span>
          </div>
        </div>

        <div>
          <div ref="panelList" class="panel-list">
            <div class="panel-list-item">
<<<<<<< HEAD
              <label>
                <div>
                  <input type="checkbox" class="panel-checkbox" v-model="selectAll" @change="toggleSelectAll" />
                  Select All
                </div>
              </label>

=======
              <label >
                <div>
                  <input
                    type="checkbox"
                    class="panel-checkbox"
                    v-model="selectAll"
                    @change="toggleSelectAll"
                  />
                  Select All
                </div>
              </label>
              
>>>>>>> 76eee5c (fixed filter issues)
            </div>
            <div v-for="(item, k) in filteredSortedUniqueValueList.slice(0, nFilterCount)" :key="k"
              class="panel-list-item">
              <!-- <input type="checkbox" class="panel-checkbox" :id="'checkbox-'+k" :value="item" v-model="selectedItems" /> -->
              <!-- <span>{{ item }}</span> -->
              <!-- <label :for="'checkbox-'+k">{{ item }}</label> -->
              <label>
                <div>
<<<<<<< HEAD
                  <input type="checkbox" class="panel-checkbox" :value="item" v-model="selectedItems"
                    @change="checkSelectAll" />
=======
                  <input type="checkbox" class="panel-checkbox" :value="item" v-model="selectedItems" @change="checkSelectAll"/>
>>>>>>> 76eee5c (fixed filter issues)
                  <!-- <input type="checkbox" class="panel-checkbox" :value="item" v-model="selectedItems" :checked="selectedItems.includes(item)" /> -->
                  <!-- <input
                    type="checkbox"
                    class="panel-checkbox"
                    :value="item"
                    :checked="selectedItems.includes(item)"
                    @change="updateSelectedList(item, $event.target.checked)"
                  /> -->
                  {{ item }}
                </div>
              </label>
            </div>
          </div>
          <div v-if="filteredSortedUniqueValueList.length > nFilterCount" class="normal-text" style="float:right">
            <span v-html="localizedLabel.listFirstNValuesOnly(nFilterCount)" />
          </div>
        </div>
      </div>

      <div class="panel-footer">
        <button class="panel-button" @click="doFilter">
          <svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="sign-in-alt" role="img"
            xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"
            class="svg-inline--fa fa-sign-in-alt fa-w-16 fa-fw fa-sm">
            <path fill="currentColor"
              d="M416 448h-84c-6.6 0-12-5.4-12-12v-40c0-6.6 5.4-12 12-12h84c17.7 0 32-14.3 32-32V160c0-17.7-14.3-32-32-32h-84c-6.6 0-12-5.4-12-12V76c0-6.6 5.4-12 12-12h84c53 0 96 43 96 96v192c0 53-43 96-96 96zm-47-201L201 79c-15-15-41-4.5-41 17v96H24c-13.3 0-24 10.7-24 24v96c0 13.3 10.7 24 24 24h136v96c0 21.5 26 32 41 17l168-168c9.3-9.4 9.3-24.6 0-34z"
              class=""></path>
          </svg>

          <span v-html="localizedLabel.apply" />
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    nFilterCount: { type: Number, default: 1000 },
    localizedLabel: {
      type: Object,
      default() {
        return {
          sortingAndFiltering: 'Sorting And Filtering',
          sortAscending: 'Sort Ascending',
          sortDescending: 'Sort Descending',
          near: '≒ Near',
          exactMatch: '= Exact Match',
          notMatch: '≠ Not Match',
          greaterThan: '&gt; Greater Than',
          greaterThanOrEqualTo: '≥ Greater Than or Equal To',
          lessThan: '&lt; Less Than',
          lessThanOrEqualTo: '≤ Less Than Or Equal To',
          regularExpression: '~ Regular Expression',
          customFilter: 'Custom Filter',
          listFirstNValuesOnly: n => `List first ${n} values only`,
          apply: 'Apply',
          freezeColumn: 'Freeze Column',
          unFreezeColumn: 'UnFreeze Column'
        }
      }
    }
  },
  data() {
    return {
      show: false,
      showDropdown: false,
      processing: false,
      columnFilterRef: null,
      inputFilter: '',
      inputFilterCondition: '',
      sortedUniqueValueList: [],
      selectedItems: [],
      selectAll: false,
      isSticky:false
    }
  },
  watch: {
    '$parent.columnFilter': {
      handler(newValue) {
        if (Object.keys(newValue).length === 0) {
          this.selectedItems = [];
        }
      },
      deep: true
    }
  },

  computed: {
    // filteredSortedUniqueValueList() {
    //   console.log("input filter selected",this.inputFilterCondition);
    //   const filter = this.inputFilter.toUpperCase()
    //   return this.sortedUniqueValueList.filter(item => item.toUpperCase().includes(filter))
    // },
    filteredSortedUniqueValueList() {
<<<<<<< HEAD
    const filter = this.inputFilter.toUpperCase();
=======
    // const filter = this.inputFilter.toUpperCase();
    const filter = this.inputFilter;
>>>>>>> 76eee5c (fixed filter issues)
    const condition = this.inputFilterCondition; // Store the selected filter condition

    return this.sortedUniqueValueList.filter(item => {
      if (!filter) return true; // Show everything if no input exists
      if (condition === "=") return item == filter; // Exact match
      if (condition === "<") return parseFloat(item) < parseFloat(filter); // Less than
      if (condition === "<=") return parseFloat(item) <= parseFloat(filter); // Less than or equal to
      if (condition === ">") return parseFloat(item) > parseFloat(filter); // Greater than
      if (condition === ">=") return parseFloat(item) >= parseFloat(filter); // Greater than or equal to
      if (condition === "<>") return item != filter; // Not match
      if (condition === "~") return new RegExp(filter).test(item); // Regular Expression match

      return item.toUpperCase().includes(filter.toUpperCase()); // Default: Partial match
<<<<<<< HEAD
=======
      // return item.includes(filter.trim());
>>>>>>> 76eee5c (fixed filter issues)
    });
  },


    symbol() {
      switch (this.inputFilterCondition) {
        case '': return '≒'
        case '<=': return '≤'
        case '>=': return '≥'
        case '<>': return '≠'
        default: return this.inputFilterCondition
      }
    },
  },
  methods: {
    toggleSelectAll() {
    if (this.selectAll) {
      this.selectedItems = [...this.sortedUniqueValueList]; // Select all items
    } else {
      this.selectedItems = []; // Deselect all items
    }
  },
    checkSelectAll() {
      // If any checkbox is unchecked, deselect "Select All"
      this.selectAll = this.selectedItems.length === this.filteredSortedUniqueValueList.length;
    },


    clickOutside(e) {
      if (e.target.id === 'panelModal') this.hidePanel()
    },
    sort(direction) {
      this.hidePanel()
      this.$parent.sort(direction, this.columnFilterRef.colPos)
    },
    freezeOrUnFreezeColumn(){
      this.hidePanel()
      this.$parent.freezeOrUnFreezeColumn(this.columnFilterRef.colPos);
    },
    setFilterCondition(choice) {
      this.showDropdown = false
      this.inputFilterCondition = choice
      this.$refs.inputFilter.focus()
    },
    freezePanelSizeAfterShown() {
      const target = this.$refs.panelList
      console.log("target",target);
      const rect = target.getBoundingClientRect()
      console.log("Rect",rect);
      target.setAttribute('style', `width:${rect.width}px; height:${rect.height}px;`)
    },
    removePanelSizeAfterHide() {
      const target = this.$refs.panelList
      target.removeAttribute('style')
    },
    doInputFilter() {
      if (window.delay) clearTimeout(window.delay)
      window.delay = setTimeout(() => {
        this.inputFilter = this.$refs.inputFilter.value
      }, 200)
    },
    // doFilter() {
    //   let opt
    //   if (this.selectedItems.length > 0) {
    //     // 🔥 Updated to support multi-select
    //     opt = this.selectedItems.map(i => `${this.inputFilterCondition}${i}`).join(',')
    //     // Handle multiple selected items correctly for filtering
    //     // this.filteredSortedUniqueValueList = this.filteredSortedUniqueValueList.filter(item =>
    //     //   this.selectedItems.includes(item)
    //     // );
    //     // opt = this.selectedItems;
    //   } else {
    //     opt = this.inputFilterCondition + this.$refs.inputFilter.value
    //   }
    //   this.columnFilterRef.$el.textContent = opt
    //   this.columnFilterRef.$emit('update:modelValue', opt)
    //   this.hidePanel()
    // },

    // doFilter() {
    //   let opt
    //   if (this.selectedItems.length > 0) {
    //     opt = this.selectedItems // send as raw array
    //   } else {
    //     opt = this.inputFilterCondition + this.$refs.inputFilter.value
    //   }

    //   this.columnFilterRef.$el.textContent = Array.isArray(opt) ? opt.join(', ') : opt
    //   this.columnFilterRef.$emit('update:modelValue', opt)
    //   this.hidePanel()
    // },

    doFilter() {
      if (this.selectedItems.length > 0) {
        // Create a special format that the parent component will recognize
<<<<<<< HEAD
        console.log("selected items",this.selectedItems);
=======
        // console.log("selected items",this.selectedItems);
>>>>>>> 76eee5c (fixed filter issues)
        const opt = `in:${this.selectedItems.join(',')}`
        // Display the selected items in the UI
        this.columnFilterRef.$el.textContent = this.selectedItems.join(', ')

        // Send the filter expression to the parent
        this.columnFilterRef.$emit('update:modelValue', opt)
      } else {
        // Handle single filter case
        const opt = this.inputFilterCondition + this.$refs.inputFilter.value
        this.columnFilterRef.$el.textContent = opt
        this.columnFilterRef.$emit('update:modelValue', opt)
      }

      this.hidePanel()
    },

    filterPanelSelect(opt) {
      // 🔥 Optional: no longer used directly for single select
    },
    showPanel(ref) {
<<<<<<< HEAD
      console.log("selected items",this.selectedItems);
=======
      // console.log("selected items",this.selectedItems);
>>>>>>> 76eee5c (fixed filter issues)
      this.columnFilterRef = ref
      this.inputFilter = ''
      this.inputFilterCondition = ''
      // this.selectedItems = [] 
      this.sortedUniqueValueList = []
      this.$refs.inputFilter.value = ''
      this.isSticky =  this.$parent.isSticky(this.columnFilterRef.colPos);
      this.$parent.focused = false;
      // if (this.columnFilterRef.$el.textContent !== '') {
      //   console.log(this.columnFilterRef.$el.textContent);
      //   this.columnFilterRef.$el.textContent = ''
      //   this.columnFilterRef.$emit('update:modelValue', '')
      //   this.$parent.calTable()
      // }
      setTimeout(() => {
        this.show = true
        setTimeout(() => (this.$refs.inputFilter.focus()))

        const hash = {}
        const fieldName = this.$parent.fields[ref.colPos].name
        // this.$parent.table.forEach(record => (hash[record[fieldName]] = true))
        this.$parent.modelValue.forEach(record => (hash[record[fieldName]] = true))
<<<<<<< HEAD

=======
        // this.$parent.modelValue.forEach(record => (hash[record[fieldName]?.trim()] = true));
        // console.log("modelvalue",this.$parent.modelValue);
>>>>>>> 76eee5c (fixed filter issues)
        const keys = Object.keys(hash)
        // keys.sort()
        keys.sort((a, b) => {
      const aSelected = this.selectedItems.includes(a);
      const bSelected = this.selectedItems.includes(b);
      
      if (aSelected && !bSelected) return -1; // Selected comes first
      if (!aSelected && bSelected) return 1;  // Unselected comes later
      return a.localeCompare(b); // Sort remaining items alphabetically
    });
        if (keys.length > 0 && keys[0] === '') keys[0] = ' '
        this.sortedUniqueValueList = keys
<<<<<<< HEAD
        console.log("field name",fieldName);
        console.log("keys",keys);
=======
        // console.log("field name",fieldName);
        // console.log("keys",keys);
>>>>>>> 76eee5c (fixed filter issues)
        // this.selectedItems = [...this.filteredSortedUniqueValueList]; // Pre-select items
        setTimeout(() => this.freezePanelSizeAfterShown())
      })
    },
    hidePanel() {
      this.show = false
      this.$parent.focused = true;
      this.removePanelSizeAfterHide()
      setTimeout(() => {
        this.sortedUniqueValueList = []
        // this.selectedItems = []
      }, 0)
    }
  }
}
</script>
<style scoped>

input:focus, button:focus {
  outline: none !important;
  box-shadow: none !important;
}

.panel-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  background-color: #0007;
  z-index: 999;
  font-weight: 400;
  font-size: 1rem;
  text-shadow: none;
}

.panel-body {
  background-color: white;
  position: fixed;
  border-radius: 5px;
  padding: 0;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  max-width: 75vh;
  height: fit-content;
  max-height: 80vh;
  display: flex;
  flex-direction: column;
}

.panel-title {
  padding: 1rem;
  display: flex;
  color: dimgray;
  font-size: 1.25rem;
  line-height: 1.5rem;
  align-items: center;
  justify-content: flex-start;
  border-bottom: 1px solid lightgray;
}

div.panel-title span, button.panel-button span {
  margin-left: 6px;
  vertical-align: text-top;
}

.panel-content {
  padding: 1rem;
  text-align: left;
  overflow-y: scroll;
}

.panel-content .panel-button {
  width: 48%;
  background-color: #17a2b8;
}

.panel-action {
  display: inline-block;
  margin-bottom: 0.5rem;
  width: 100%;
  position: relative;
  white-space: nowrap;
}

.panel-input-b {
  display: inline-block;
  border-top-right-radius: 4px;
  border-bottom-right-radius: 4px;
  width: calc(100% - 2.2rem);
  border: 1px solid lightgray;
  border-left: 0;
  margin-left: -4px;
  height: 2.3rem;
}
.panel-input {
  border: 0;
  box-shadow: none;
  padding: 0.6rem;
  width: calc(100% - 2.2rem);
  font-size: 0.88rem;
  background-color: transparent
}
.panel-input-button {
  border-top-left-radius: 4px;
  border-bottom-left-radius: 4px;
  color: white;
  background-color: #28a745;
  border: 1px solid #28a745;
  font-size: 1.3rem;
  width: 2.2rem;
  height: 2.35rem;
  vertical-align: -2px;
  cursor: pointer;
}

.panel-dropdown {
  z-index: 50;
  position: absolute;
  left: 0;
  top: 2.4rem;
  display: inline-block;
  background-color: white;
  border: 1px solid gray;
  margin-top: -1px;
  display: none;
}

.panel-dropdown.show {
  display: inline-block;
}
.panel-dropdown-item {
  padding: 0.35rem 0.65rem;
  cursor: pointer;
}
.panel-dropdown-item:hover {
  background-color: lightskyblue;
}
.panel-dropdown-item span {
  margin-right: 6px;
  color: gray;
}
.panel-dropdown-item:not(:last-child) {
  border-bottom: 1px solid lightgray;
}

.panel-footer {
  display: flex;
  padding: 1rem;
  align-items: center;
  justify-content: flex-end;
  border-top: 1px solid lightgray;
}

.panel-button {
  width: 120px;
  font-size: 0.88rem;
  border-radius: 5px;
  border: 0;
  background-color: #007bff;
  color: white;
  padding: 0.6rem;
  cursor: pointer;
}

.float-left {
  float: left !important;
}

.float-right {
  float: right !important;
}
.float-middle {
  display: block;
  margin-left: auto;
  margin-right: auto;
}

.panel-list {
  overflow-y: scroll;
  max-height: 20rem;
  border: 1px solid #ced4da;
  border-radius: 0.25rem;
  display: flex;
  flex-direction: column;
}
.panel-checkbox {
  vertical-align: bottom;
}
.panel-list span {
  margin-left: 10px;
  color: gray;
}
.panel-list-item {
  padding: 10px 10px;
  font-size: 0.88rem;
  cursor: pointer;
  white-space: nowrap;
}
.panel-list-item:hover {
  background-color: lightskyblue;
}
.panel-list-item:not(:last-child) {
  border-bottom: 1px solid lightgray;
}
.normal-text {
  font-size: 0.88rem;
  color: gray;
}

.fa-spin {
  -webkit-animation: fa-spin 2s infinite linear;
  animation: fa-spin 2s infinite linear;
}
.svg-inline--fa.fa-w-14 {
  width: 0.875em;
}
.svg-inline--fa.fa-w-16 {
  width: 1em;
}
.svg-inline--fa.fa-fw {
  width: 1.25em;
}
.svg-inline--fa {
  display: inline-block;
  font-size: inherit;
  height: 1em;
  overflow: visible;
  vertical-align: -0.125em;
}
.fa-fw {
  text-align: center;
  width: 1.25em;
}
.fa-xs {
  font-size: 0.75em;
}
.fa-sm {
  font-size: 0.875em;
}
.fa-1x {
  font-size: 1em;
}
.fa-2x {
  font-size: 2em;
}
.fa-3x {
  font-size: 3em;
}
</style>
