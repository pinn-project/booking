<template>
  <div class="ui--input">

    <label :for="name" :class="['ui--input-label', { required }]">
      <i v-if="icon" :class="`ion-${icon}`"></i>
      <span>{{ label }}</span>
    </label>

    <textarea
      v-if="type === 'textarea'"
      v-model.trim="currentValue"
      :id="name"
      class="ui--input-textarea">
    </textarea>

    <input
      v-else
      :id="name"
      :type="type"
      :maxlength="maxlength"
      v-model.trim="currentValue"
      autocomplete="off"
      class="ui--input-default">

  </div>
</template>

<script lang="ts">
import { Vue, Prop, Watch, Component } from 'vue-property-decorator'

@Component
export default class Input extends Vue {
  @Prop(String) value!: any
  @Prop(String) readonly name!: string
  @Prop(String) readonly type!: string
  @Prop(String) readonly label!: string
  @Prop(String) readonly icon!: string
  @Prop(Number) readonly maxlength!: number
  @Prop(Boolean) readonly required!: boolean

  // __DATA
  private currentValue: string = this.value || ''

  // __WATCH
  @Watch('value')
  private onValue (value: any): void {
    this.currentValue = value
  }

  @Watch('currentValue')
  private onEmit (value: any): void {
    this.$emit('input', this.currentValue)
  }
}
</script>