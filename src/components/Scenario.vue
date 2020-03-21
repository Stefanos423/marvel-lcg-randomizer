<template>
    <div class="scenario-randomizer panel" v-if="scenario">
        <div class="title panel-insert" @click="shown=!shown">Scenario</div>
        <div class="content" v-if="shown">
            <div>
                <div class="horizontal-card">
                    <img :src="scenario.scenario.img" :alt="scenario.scenario.name">
                    <div class="panel-insert-content">
                        {{scenario.scenario.name}}({{scenario.scenario.pack}})
                    </div>
                </div>
                <div v-bind:key="index" v-for="({deck, modules}, index) in scenario.modules">
                    <div v-if="modules.length > 0">
                        <div v-if="scenario.modules.length > 1">Deck {{deck.name}}</div>
                        <div class="horizontal-card" :key="index2" v-for="(mod, index2) in modules">
                            <img :src="mod.img" :alt="mod.name"/>
                            <div class="panel-insert-content">
                                {{mod.name}}({{mod.pack}})
                            </div>
                        </div>
                    </div>
                </div>
                <div v-if="environment">
                    <img :src="environment.img" :alt="environment.name"/>
                </div>
            </div>
            <div class="difficulty panel-insert-content">
                Difficulty:
                <span class="difficulty-value">
                    {{scenario.difficulty}}
                </span>
            </div>
        </div>

    </div>
</template>

<script>
    export default {
        name: "Scenario.vue",
        props: {
            scenario: {
                required: true,
            },
            environment: {
                default: {}
            }
        },
        data() {
            return {
                shown: true,
            };
        },
    }
</script>

<style scoped>
    img {
        box-sizing: border-box;
        width: 100%;
        max-width: 300px;
        padding: 0 10px;
    }

    .difficulty-value {
        font-weight: bold;
    }

    .content {
        text-align: center;
    }

    .horizontal-card {
        display: flex;
        flex-direction: column !important;
        justify-content: center !important;
        align-items: center !important;
    }
</style>
