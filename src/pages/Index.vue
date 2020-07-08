<template>
  <q-page>

    <!-- form building -->
    <q-form-builder v-model="fields" />

    <q-separator />

    <!-- form rendering -->
    <div class="q-pa-md q-form-container">
      <h4>Form Rendering</h4>
      <div v-for="(field, index) in fields" :key="index">
        <component v-model="fieldData[field.cid]" @input="onInput" v-bind:is="getElement(field)" :label="field.label" :required="field.required" :field_options="field.field_options" :id="field.cid" :cid="field.cid" :ref="field.cid" debounce="500" />
      </div>
    </div>

  </q-page>
</template>

<script>

import { QFormBuilder, TextElement, ParagraphElement, CheckboxesElement, RadioElement, DateElement, TimeElement, DropdownElement, EmailElement, NameElement, SimpleNameElement, AddressElement, PhoneElement, FileElement, PaymentElement, TermsElement, PageBreakElement, SectionBreakElement } from 'q-form-builder'

export default {
  name: 'SampleApp',
  components: {
    QFormBuilder,
    TextElement,
    ParagraphElement,
    CheckboxesElement,
    RadioElement,
    DateElement,
    TimeElement,
    DropdownElement,
    EmailElement,
    NameElement,
    SimpleNameElement,
    AddressElement,
    PhoneElement,
    FileElement,
    PaymentElement,
    TermsElement,
    PageBreakElement,
    SectionBreakElement
  },
  data: function () {
    return {
      fields: [],
      fieldData: []
    }
  },
  methods: {
    /**
     * When a value is input into the rendered form, echo it to the debug line
     */
    onInput (val, id) {
      // console.debug(`${id}: ` + JSON.stringify(val))
    },
    /**
     * Determine the name of the Element object based on the 'field_type' of the field data object
     */
    getElement (field) {
      const nameParts = field.field_type.split('_')
      for (let i = 0; i < nameParts.length; i++) {
        nameParts[i] = nameParts[i].charAt(0).toUpperCase() + nameParts[i].slice(1)
      }
      return nameParts.join('') + 'Element'
    }
  },
  watch: {
    fields: {
      handler (val) {
        // console.debug(val)
      },
      deep: true
    }
  }
}
</script>

<style lang="stylus">

  .source-field
    width 129px
    display inline-block
    margin 0px 2px 5px 2px
    .q-btn
      width 100%

  .q-page
    padding 20px

  .q-form-builder-elements-container
    width 100%
    min-height 200px

  .q-form-builder-elements-container.empty
    background-image url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' version='1.1' height='200px' width='500px'><text x='0' y='15' fill='lightgray' font-size='14' font-family='Roboto, Helvetica, sans-serif'>Drag an element here to get started.</text></svg>")
    background-repeat no-repeat
    background-position 0 40px

  .q-editable-element.selected
    background-color $blue-grey-1

  .editable-element-container
    position relative

  .editable-element-action-buttons
    position absolute
    bottom -11 px
    right 0
    z-index 2

  .editable-element-button
    float right
    margin-right 5px

  .q-form-container
    max-width 820px
    margin auto
</style>
