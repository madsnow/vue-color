<template>
    <div role="application" aria-label="light color picker"
         :class="['vc-light']">
        <div class="vc-light-fields-wrap">
            <slot name="extra-fields"></slot>
            <div class="vc-light-fields">
                <div class="vc-light-field">
                    <ed-in label="hex" :value="colors.hex" @change="inputChange"
                           :show-desc="false"
                           :show-label="false"></ed-in>
                </div>
            </div>
        </div>

        <div class="vc-light-saturation-wrap">
            <saturation v-model="colors" @change="childChange"></saturation>
        </div>

        <div class="vc-light-body">
            <div class="vc-light-controls">
                <div class="vc-light-sliders">
                    <div class="vc-light-hue-wrap">
                        <hue v-model="colors" @change="childChange"></hue>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import colorMixin from '../mixin/color'
import editableInput from './common/EditableInput.vue'
import saturation from './common/Saturation.vue'
import hue from './common/Hue.vue'

export default {
    name: 'Light',
    mixins: [colorMixin],
    components: {
        saturation,
        hue,
        'ed-in': editableInput
    },
    data () {
        return {
            fieldsIndex: 0,
            highlight: false
        }
    },

    methods: {
        childChange (data) {
            this.colorChange(data)
        },
        inputChange (data) {
            if (!data) {
                return
            }
            if (data.hex) {
                this.isValidHex(data.hex) && this.colorChange({
                    hex: data.hex,
                    source: 'hex'
                })
            }
        }
    }
}
</script>

<style>
.vc-light {
    border-radius: 2px;
    box-shadow: 0 0 2px rgba(0, 0, 0, .3), 0 4px 8px rgba(0, 0, 0, .3);
    box-sizing: initial;
    width: 225px;
    background-color: #fff;
}

.vc-light-controls {
    display: flex;
}


.vc-light-sliders {
    flex: 1;
}

.vc-light-fields-wrap {
    display: flex;
    padding-top: 16px;
}

.vc-light-fields {
    display: flex;
    margin-left: -6px;
    flex: 1;
}

.vc-light-field {
    padding-left: 6px;
    width: 100%;
}

.vc-light-hue-wrap {
    position: relative;
    height: 10px;
    margin-bottom: 0;
}

.vc-light-body {
    padding: 10px 10px;
    background-color: #000;
}

.vc-light-saturation-wrap {
    width: 100%;
    padding-bottom: 55%;
    position: relative;
    border-radius: 2px 2px 0 0;
    overflow: hidden;
}

.vc-light__disable-alpha .vc-light-hue-wrap {
    margin-top: 4px;
    margin-bottom: 4px;
}
</style>
