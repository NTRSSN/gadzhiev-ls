<template>
    <div class="skill-component" v-if="editmode === false">
        <div class="title">{{skill.title}}</div>
        <div class="percent">{{skill.percent}} %</div>
        <div class="buttons">
            <icon symbol="pencil" class="btn" @click="editmode = true" grayscale />
            <icon symbol="trash" class="btn" @click="$emit('remove', skill.id)" grayscale />
        </div>
    </div>
    
    <div class="skill-component" v-else>
        <div class="title">
            <app-input noSidePaddings v-model="currentSkill.title" />
            <div class="message">{{ validation.firstError('currentSkill.title') }}</div>
        </div>
        <div class="percent">
            <app-input v-model="currentSkill.percent" type="number" min="0" max="100" maxlength="3" />
            <div class="message">{{ validation.firstError('currentSkill.percent') }}</div>
        </div>
        <div class="buttons">
            <icon symbol="tick" class="btn" @click="submitHandler"/>
            <icon symbol="cross" class="btn" @click="editmode = false" />
        </div>
    </div>
</template>

<script>
import input from "../input";
import icon from "../icon";
import SimpleVueValidator from 'simple-vue-validator';

const Validator = SimpleVueValidator.Validator;

export default {
    mixins: [SimpleVueValidator.mixin],
    validators: {
        'currentSkill.title': function(value) {
            return Validator.value(value).required();
        },
        'currentSkill.percent': function(value) {
            return Validator.value(value).required();
        }
    },
    props: {
        skill: {
            type: Object,
            default: () => {},
            required: true
        }
    },
    data() {
        return {
            editmode: false,
            currentSkill: {
                id: 0,
                title: this.skill.title,
                percent: this.skill.percent
            }
        }
    },
    components: {
        icon,
        appInput: input
    },
    methods: {
        submitHandler() {
            this.$validate().then(success => {
                console.log('1')
                if (success) {
                    console.log('2')
                this.$emit("approve", this.currentSkill)
                }
            })
        }
    }
}
</script>

<style lang="postcss" src="./skill.pcss" scoped>
    
</style>