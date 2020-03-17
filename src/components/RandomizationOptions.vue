<template>
    <div class="panel">
        <div class="panel-insert">
            Custom Options
        </div>
        <div v-if="shown" class='custom-options'>
            <div>
                <button :disabled="customOptions.additionalModules <= 0" @click="additionalModulesChange((customOptions.additionalModules || 0) - 1)">-</button>
                {{ customOptions.additionalModules || 0 }}
                <button @click="additionalModulesChange(parseInt(customOptions.additionalModules || 0) + 1)">+</button>
                Extra Modules
            </div>

            <div>
                <input type="checkbox" @input="toggleCustomEnvironments($event.target.checked)">Custom Environments
            </div>

            <div @click="shown=!shown" class="panel-insert-content">
                Hide Options
            </div>
        </div>
        <div v-else>
            <div @click="shown=!shown" class="panel-insert-content">
                Show Options
            </div>
        </div>

    </div>
</template>

<script>
    export default {
        name: "RandomizationOptions",
        props: {
            customOptions: {
                default: {},
            },
        },
        data: () => ({
            shown: false,
        }),
        methods: {
            additionalModulesChange(modules) {
                this.customOptions = {...this.customOptions};
                this.customOptions.additionalModules = modules;
                this.$emit("input", this.customOptions);
            },
            toggleCustomEnvironments(shouldIncludeCustomEnvironments) {
                this.customOptions = {...this.customOptions};
                this.customOptions.shouldIncludeCustomEnvironments = shouldIncludeCustomEnvironments;
                this.$emit("input", this.customOptions);
            }
        },
    }
</script>

<style scoped>
    .custom-options {
        display: flex;
        justify-content: space-evenly;
        flex-wrap: wrap;
    }
    
    .custom-options div {
        margin: auto
    }
</style>
