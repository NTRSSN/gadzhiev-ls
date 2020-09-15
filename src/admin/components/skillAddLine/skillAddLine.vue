<template>    
    <div 
        :class="['skill-add-line-component', {blocked: blocked}]"
    >
        <div class="title">
            <app-input v-model="newSkillTitle" placeholder="Новый навык" />
            <div class="message">{{ validation.firstError('newSkillTitle') }}</div>
        </div>
        <div class="percent">
            <app-input v-model="newSkillPercent" type="number" min="0" max="100" maxlength="3" />
            <div class="message">{{ validation.firstError('newSkillPercent') }}</div>
        </div>
            <iconed-button type="round" title="" />
    </div>
</template>

<script>
import input from "../input";
import button from "../button";
import SimpleVueValidator from 'simple-vue-validator';

const Validator = SimpleVueValidator.Validator;

export default {
    mixins: [SimpleVueValidator.mixin],
    validators: {
        'newSkillTitle': function(value) {
            return Validator.value(value).required();
        },
        'newSkillPercent': function(value) {
            return Validator.value(value).required();
        },
    },
    props: {
        blocked: Boolean
    },
    components: {
        appInput: input,
        iconedButton: button
    },
    data() {
        return {
            newSkillTitle: "",
            newSkillPercent: ""
        }
    }
}
</script>

<style lang="postcss" src="./skillAddLine.pcss" scoped>
    
</style>