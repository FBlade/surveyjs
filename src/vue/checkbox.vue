<template>
    <form :class="css.checkbox.root">
        <div v-for="(item, index) in question.visibleChoices" :class="css.radiogroup.item" :style="{width: colWidth, 'margin-right': question.colCount === 0 ? '5px': '0px'}">
            <label :class="css.radiogroup.item">
                <input type="checkbox" :name="question.name" :value="item.value" v-model="value" :id="question.inputId + '_' + item.value" :disabled="!isEditMode" />
                <span>{{item.text}}</span>
                <survey-other-choice v-show="question.hasOther && question.isOtherSelected" :class="css.radiogroup.other" :question="question" :isEditMode="isEditMode" :css="css"/>
            </label>
        </div>
    </form>
</template>

<script lang="ts">
    import * as Vue from 'vue'
    import {Component, Prop, Watch} from 'vue-property-decorator'
    import {default as Question} from './question'
    import {QuestionCheckboxModel} from '../question_checkbox'

    @Component
    export default class Checkbox extends Question<QuestionCheckboxModel> {
        get value() {
            return this.question.value || [];
        }
        set value(newVal) {
            this.question.value = newVal;
        }
        get colWidth() {
            var colCount = this.question.colCount;
            return colCount > 0 ? (100 / colCount) + '%' : "";
        }
    }
    Vue.component("survey-checkbox", Checkbox)
</script>