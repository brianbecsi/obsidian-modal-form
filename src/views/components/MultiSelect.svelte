<script lang="ts">
    import type { App, Setting } from "obsidian";
    import { remove_inplace } from "../../utils/array";
    import { MultiSuggest } from "../../suggesters/MultiSuggest";

    export let selectedVales: string[] = [];
    export let availableOptions: string[] = [];
    // We take the setting to make it consistent with the other input components
    export let setting: Setting;
    export let app: App;

    setting.settingEl.setCssStyles({
        alignItems: "baseline",
    });

    let remainingOptions = new Set(availableOptions);

    function createInput(element: HTMLInputElement) {
        new MultiSuggest(
            element,
            remainingOptions,
            (selected) => {
                selectedVales.push(selected);
                remainingOptions.delete(selected);
                selectedVales = selectedVales;
            },
            app
        );
    }
    function reomoveValue(value: string) {
        remove_inplace(selectedVales, value);
        selectedVales = selectedVales;
        remainingOptions.add(value);
    }
</script>

<div class="multi-select-root">
    <input
        use:createInput
        type="text"
        class="form-control"
        placeholder="Select"
    />
    <div class="badges">
        {#each selectedVales as value}
            <div class="badge">
                <span>{value}</span>
                <button on:click={() => reomoveValue(value)}>
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        width="24"
                        height="24"
                        viewBox="0 0 24 24"
                        fill="none"
                        stroke="currentColor"
                        stroke-width="2"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        class="svg-icon lucide-x"
                        ><line x1="18" y1="6" x2="6" y2="18" /><line
                            x1="6"
                            y1="6"
                            x2="18"
                            y2="18"
                        /></svg
                    ></button
                >
            </div>
        {:else}
            <div class="badge hidden">
                <span>Nothing selected</span>
            </div>
        {/each}
    </div>
</div>

<style>
    .multi-select-root {
        display: flex;
        flex-direction: column;
        gap: 0.5rem;
        flex: 1;
        --button-size: 1.5rem;
    }
    .badge {
        --icon-size: var(--icon-xs);
        --icon-stroke: var(--icon-xs-stroke-width);
        display: flex;
        align-items: center;
        background-color: var(--pill-background);
        border: var(--pill-border-width) solid var(--pill-border-color);
        border-radius: var(--pill-radius);
        color: var(--pill-color);
        cursor: var(--cursor);
        font-weight: var(--pill-weight);
        padding: var(--pill-padding-y);
        line-height: 1;
        max-width: 100%;
        gap: var(--size-4-2);
        justify-content: center;
        align-items: center;
    }
    .hidden {
        visibility: hidden;
    }
    .hidden span {
        height: var(--button-size);
    }
    .badge span {
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
        min-width: 1rem;
    }
    .badges {
        display: flex;
        flex-wrap: wrap;
        gap: 8px;
        min-height: 2rem;
        padding: 0.5rem 0 0 0;
    }
    button {
        /* reset button styles */

        background: none;
        border: none;
        color: inherit;
        font: inherit;
        line-height: inherit;
        padding: 0;
        -webkit-appearance: none;
        -moz-appearance: none;
        -o-appearance: none;
        appearance: none;
        box-shadow: none;
        border: none;
        cursor: pointer;
        height: var(--button-size);
        width: var(--button-size);
    }
</style>
