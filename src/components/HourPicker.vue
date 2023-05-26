<template>
  <div class="hour-picker">
    <div class="hour-picker-header">
      <!-- Hours -->
      <div class="position-relative">
        <button
          type="button"
          class="hour-picker-action"
          @click="showHours = true"
        >
          {{ currentTime.hour }}
        </button>
        <div class="select-content" v-if="showHours">
          <button
            type="button"
            v-for="item in hours"
            :key="item.label"
            @click="setHour(item)"
          >
            {{ item.label }}
          </button>
        </div>

        <div class="overlay" @click="showHours = false" v-if="showHours"></div>
      </div>

      <span class="separator">:</span>

      <!-- Minutes -->
      <div class="position-relative">
        <button
          type="button"
          class="hour-picker-action"
          @click="showMinutes = true"
        >
          {{ currentTime.minutes }}
        </button>
        <div class="select-content select-content-scroll" v-if="showMinutes">
          <button
            type="button"
            v-for="item in minutes"
            :key="item.label"
            @click="setMinutes(item)"
          >
            {{ item.label }}
          </button>
        </div>

        <div
          class="overlay"
          @click="showMinutes = false"
          v-if="showMinutes"
        ></div>
      </div>

      <button
        type="button"
        class="time-period hour-picker-action"
        @click="changeTimePeriod()"
      >
        {{ timePeriod }}
      </button>
    </div>

    <!-- <div class="clock-container">
      <div class="clock"></div>
    </div> -->
  </div>
</template>

<script>
export default {
  name: "HourPicker",
  data() {
    return {
      timePeriod: "AM",
      showHours: false,
      showMinutes: false,
      hours: [],
      minutes: [],
      currentTime: {
        hour: "01",
        minutes: "00"
      },
    };
  },
  mounted() {
    this.generateHours();
    this.generateMinutes();
  },
  methods: {
    generateHours() {
      let initial = "00";

      for (let i = 1; i <= 12; i++) {
        initial = `${initial[1]}${i}`;

        if (initial.length == 3) {
          initial = initial.substr(1, 2);
        }

        this.hours.push({
          label: initial,
        });

        initial = "00";
      }
    },
    generateMinutes() {
      let initial = "00";

      for (let i = 0; i <= 59; i++) {
        initial = `${initial[1]}${i}`;

        if (initial.length == 3) {
          initial = initial.substr(1, 2);
        }

        this.minutes.push({
          label: initial,
        });

        initial = "00";
      }
    },
    setHour(item) {
      this.currentTime.hour = item.label;
      this.showHours = false;
    },
    setMinutes(item) {
      this.currentTime.minutes = item.label;
      this.showMinutes = false;
    },
    changeTimePeriod() {
      if (this.timePeriod == "AM") {
        this.timePeriod = "PM";
      } else {
        this.timePeriod = "AM";
      }
    },
  },
};
</script>

<style lang="scss">
$primary: #1867c0;
$dark: #283845;

.position-relative {
  position: relative;
}

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

    .hour-picker-action {
      font-size: 1.5rem;
      font-weight: 700;
      color: rgba(white, 0.85);
      background-color: transparent;
      border: none;
      cursor: pointer;

      &:hover {
        color: white;
        background-color: rgba($dark, 0.5);
        border-radius: 4px;
      }
    }

    .separator {
      font-size: 1.5rem;
      font-weight: 700;
      color: white;
      display: inline-block;
      margin: 0 2px;
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
      background-color: rgba($dark, 0.5);
      border-radius: 4px;
    }
  }

  .select-content {
    width: 110%;
    max-height: 340px;
    background-color: white;
    // padding-top: 8px;
    // padding-bottom: 8px;
    border: 1px solid rgba($dark, 0.3);
    border-radius: 4px;
    position: absolute;
    top: 120%;
    left: -5%;
    right: 0;
    z-index: 50;

    &-scroll {
        overflow-y: scroll;

        /* Estilo básico del scroll */
        &::-webkit-scrollbar {
            width: 3px; /* Ancho del scroll */
        }

        /* Estilo del track */
        &::-webkit-scrollbar-track {
            background: #f1f1f1; /* Color del fondo del track */
        }

        /* Estilo del thumb (barra deslizadora) */
        &::-webkit-scrollbar-thumb {
            background: #888; /* Color de la barra deslizadora */
            border-radius: 5px; /* Radio de los bordes de la barra deslizadora */
        }

        /* Estilo del thumb al pasar el mouse por encima */
        &::-webkit-scrollbar-thumb:hover {
            background: #555; /* Color de la barra deslizadora al pasar el mouse por encima */
        }
    }

    button {
      width: 100%;
      color: $dark;
      font-size: 0.85rem;
      text-align: center;
      display: block;
      padding: 6px 0;
      cursor: pointer;
      position: relative;
      border: none;
      border-bottom: 1px solid rgba($dark, 0.1);
      cursor: pointer;

      &:hover {
        background-color: $primary;
        color: white;
      }
    }
  }

  .overlay {
    background-color: transparent;
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 40;
  }
}
</style>
