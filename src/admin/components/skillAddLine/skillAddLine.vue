<template>    
    <div 
        :class="['skill-add-line-component', {blocked: blocked}]"
    >
        <div class="title">
            <app-input placeholder="Новый навык" />
        </div>
        <div class="percent">
            <app-input type="number" min="0" max="100" maxlength="3" />
        </div>
        <iconed-button type="round" title="" />
    </div>
</template>

<script>
import input from "../input";
import button from "../button";

export default {
    props: {
        blocked: Boolean
    },
    components: {
        appInput: input,
        iconedButton: button
    }
}
</script>

<style lang="postcss" src="./skillAddLine.pcss" scoped>
    
</style>