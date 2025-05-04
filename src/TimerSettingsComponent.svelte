<script lang="ts">
import { settings } from 'stores'

const updateWorkLen = (e: Event) => {
    const target = e.target as HTMLInputElement
    const value = parseInt(target.value)
    settings.update((s) => {
        if (value >= 1) {
            s.workLen = value
        }
        target.value = s.workLen.toString()
        return s
    })
}

const updateBreakLen = (e: Event) => {
    const target = e.target as HTMLInputElement
    const value = parseInt(target.value)
    settings.update((s) => {
        if (value >= 0) {
            s.breakLen = value
        }
        target.value = s.breakLen.toString()
        return s
    })
}

const updateInstantBreakInterval = (e: Event) => {
    const target = e.target as HTMLInputElement
    const value = parseInt(target.value)
    settings.update((s) => {
        if (value >= 0) {
            s.instantBreakInterval = value
        }
        target.value = s.instantBreakInterval.toString()
        return s
    })
}

const updateInstantBreakRandomOffset = (e: Event) => {
    const target = e.target as HTMLInputElement
    const value = parseInt(target.value)
    settings.update((s) => {
        if (value >= 0 && value <= 30) {
            s.instantBreakRandomOffset = value
        }
        target.value = s.instantBreakRandomOffset.toString()
        return s
    })
}
</script>

<div class="pomodoro-settings-wrapper">
    <div class="pomodoro-settings-list">
        <div class="pomodoro-settings-item">
            <div class="pomodoro-settings-label">Work</div>
            <div class="pomodoro-settings-control">
                <input
                    value={$settings.workLen}
                    on:change={updateWorkLen}
                    min="1"
                    type="number"
                />
                <span class="pomodoro-settings-unit">mins</span>
            </div>
        </div>
        <div class="pomodoro-settings-item">
            <div class="pomodoro-settings-label">Break</div>
            <div class="pomodoro-settings-control">
                <input
                    value={$settings.breakLen}
                    on:change={updateBreakLen}
                    min="0"
                    type="number"
                />
                <span class="pomodoro-settings-unit">mins</span>
            </div>
        </div>
        <div class="pomodoro-settings-item">
            <div class="pomodoro-settings-label">Instant Break Interval - Mean</div>
            <div class="pomodoro-settings-control">
                <input
                    value={$settings.instantBreakInterval}
                    on:change={updateInstantBreakInterval}
                    min="0"
                    type="number"
                />
                <span class="pomodoro-settings-unit">mins</span>
            </div>
        </div>
        <div class="pomodoro-settings-item">
            <div class="pomodoro-settings-label">Instant Break Interval - Offset</div>
            <div class="pomodoro-settings-control">
                <input
                    value={$settings.instantBreakRandomOffset}
                    on:change={updateInstantBreakRandomOffset}
                    min="0"
                    type="number"
                />
                <span class="pomodoro-settings-unit">%</span>
            </div>
        </div>
        <div class="pomodoro-settings-item">
            <div class="pomodoro-settings-label">Auto-start</div>
            <div class="pomodoro-settings-control">
                <input type="checkbox" bind:checked={$settings.autostart} />
            </div>
        </div>
        <div class="pomodoro-settings-item">
            <div class="pomodoro-settings-label">Notification Sound</div>
            <div class="pomodoro-settings-control">
                <input
                    type="checkbox"
                    bind:checked={$settings.notificationSound}
                />
            </div>
        </div>
        <div class="pomodoro-settings-item">
            <div class="pomodoro-settings-label">
                Prefer Saving to Task File
            </div>
            <div class="pomodoro-settings-control">
                <input type="checkbox" bind:checked={$settings.logFocused} />
            </div>
        </div>
    </div>
</div>

<style>
.pomodoro-settings-wrapper,
.pomodoro-settings-list,
.pomodoro-settings-item {
    width: 100%;
}

.pomodoro-settings-wrapper {
    border: 1px solid var(--background-modifier-border);
    border-radius: 5px;
}

.pomodoro-settings-item {
    display: flex;
    font-size: 0.9rem;
    align-items: center;
    /* height: 2rem; */
    padding: 0.5rem 1rem;
    gap: 8px;
}

.pomodoro-settings-item + .pomodoro-settings-item {
    border-top: 1px solid var(--background-modifier-border);
}

.pomodoro-settings-label {
    flex: 1;
    min-width: 0;
    white-space: normal; 
    word-break: break-word; 
    overflow-wrap: break-word; 
}

.pomodoro-settings-control {
    display: flex;
    align-items: center;
    gap: 2px;
    flex-shrink: 0;
}

.pomodoro-settings-unit {
    white-space: nowrap; 
    width: 20px; 
    align-items: left;
}

.pomodoro-settings-item input[type='number'] {
    width: 60px;
    min-width: 40px;
    font-size: 0.9rem;
    border: none;
    border-radius: 0;
    text-align: right;
    background: transparent;
}

.pomodoro-settings-item input[type='number']:active,
.pomodoro-settings-item input[type='number']:focus {
    border: none;
    box-shadow: none;
}

.pomodoro-settings-item input[type='checkbox'] {
    margin: 0;
}
</style>
