<template>
    <div class="hour-picker">
        <div class="hour-picker-header">
            <button type="button">
                12
            </button>
            <span class="separator">:</span>
            <button type="button">
                05
            </button>

            <button type="button" class="time-period">{{ timePeriod }}</button>
        </div>

        <div class="clock-container">
            <div class="clock"></div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'HourPicker',
    data() {
        return {
            timePeriod: 'AM'
        }
    }
}
</script>

<style lang="scss">
$primary: #1867c0;

.hour-picker {
    &-header {
        background-color: $primary;
        max-width: max-content;
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 0 auto;
        padding: 8px;
        border-radius: 4px;

        button {
            font-size: 1.5rem;
            font-weight: 700;
            color: rgba(white, .85);
            background-color: transparent;
            border: none;
            cursor: pointer;

            &:hover {
                color: white;
            }
        }

        .separator {
            font-size: 1.5rem;
            font-weight: 700;
            color: white;
        }
    }

    .clock-container {
        margin-top: 1rem;
    }

    .clock {
        border: 1px solid $primary;
    }

    .time-period {
        font-size: 1.5rem;
        color: white;
        display: inline-block;
        margin-left: 8px;

        &:hover {
            background-color: rgba(#283845, .5);
            border-radius: 4px;
        }
    }
}
</style>