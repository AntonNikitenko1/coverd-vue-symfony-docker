<template>
    <div>
        <form role="form">
            <div
                v-for="attribute in attributes.filter(filter)"
                :key="attribute.definition_id"
            >
                <BooleanField
                    v-if="attribute.displayInterface === 'TOGGLE'"
                    v-model="attribute.value"
                    :label="attribute.label"
                    :help-text="attribute.helpText"
                />
                <YesNoRadioField
                    v-else-if="attribute.displayInterface === 'YES_NO_RADIO'"
                    v-model="attribute.value"
                    :label="attribute.label"
                    :help-text="attribute.helpText"
                />
                <DateField
                    v-else-if="attribute.displayInterface === 'DATETIME'"
                    v-model="attribute.value"
                    :label="attribute.label"
                    :help-text="attribute.helpText"
                />
                <NumberField
                    v-else-if="attribute.displayInterface === 'NUMBER'"
                    v-model="attribute.value"
                    :label="attribute.label"
                    :help-text="attribute.helpText"
                />
                <OptionListApi
                    v-else-if="attribute.displayInterface === 'SELECT_SINGLE'"
                    v-model="attribute.value"
                    :label="attribute.label"
                    :help-text="attribute.helpText"
                    :preloaded-options="attribute.options"
                />
                <RadioField
                    v-else-if="attribute.displayInterface === 'RADIO'"
                    v-model="attribute.value"
                    :label="attribute.label"
                    :help-text="attribute.helpText"
                    :preloaded-options="attribute.options"
                />
                <TextareaField
                    v-else-if="attribute.displayInterface === 'TEXTAREA'"
                    v-model="attribute.value"
                    :label="attribute.label"
                    :help-text="attribute.helpText"
                />
                <AddressField
                    v-else-if="attribute.displayInterface === 'ADDRESS'"
                    v-model="attribute.value"
                    :label="attribute.label"
                    :help-text="attribute.helpText"
                />
                <ZipCountyField
                    v-else-if="attribute.displayInterface === 'ZIPCODE'"
                    v-model="attribute.value"
                    :label="attribute.label"
                    :help-text="attribute.helpText"
                />
                <TextField
                    v-else
                    v-model="attribute.value"
                    :label="attribute.label"
                    :help-text="attribute.helpText"
                />
            </div>
        </form>
    </div>
</template>


<script>
    import DateField from "./DateField";
    import TextField from "./TextField";
    import NumberField from "./NumberField";
    import OptionListApi from "./OptionListApi";
    import TextareaField from "./TextareaField";
    import RadioField from "./RadioField";
    import BooleanField from "./ToggleField";
    import YesNoRadioField from "./YesNoRadioField";
    import AddressField from "./AddressField";
    import ZipCountyField from "./ZipCountyField";
    export default {
        name: 'AttributesEditForm',
        components: {
            ZipCountyField,
            AddressField,
            YesNoRadioField,
            BooleanField, RadioField, TextareaField, OptionListApi, NumberField, TextField, DateField},
        props: {
            new: { type: Boolean },
            value: { type: Array, required: true },
            filter: { type: Function, required: false, default: (attribute) => true }
        },
        computed: {
            attributes: function () {
                if (this.value) {
                    let attributes = this.value;
                    return attributes.sort((a, b) => a.orderIndex - b.orderIndex)
                }

                return []
            }
        },
    }
</script>