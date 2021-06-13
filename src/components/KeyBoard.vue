<template>
  <div ref="key-board" class="key-board">
    <div class="row num-row">
      <kbd @click="pushNumOrSymbol(symbolMap[0])" class="key">
        <span :class="{ key__inactive: isShiftPressed }">
          {{ symbolMap[0].lower }}
        </span>
        <span :class="{ key__inactive: !isShiftPressed }">
          {{ symbolMap[0].upper }}
        </span>
      </kbd>
      <kbd
        @click="pushNumOrSymbol(item, true)"
        class="key"
        v-for="(item, index) in numMap"
        :key="index"
      >
        <span :class="{ key__inactive: isShiftPressed }">
          {{ item.lower }}
        </span>
        <span :class="{ key__inactive: !isShiftPressed }">
          {{ item.upper }}
        </span>
      </kbd>
      <kbd @click="pushNumOrSymbol(symbolMap[1])" class="key">
        <span :class="{ key__inactive: isShiftPressed }">
          {{ symbolMap[1].lower }}
        </span>
        <span :class="{ key__inactive: !isShiftPressed }">
          {{ symbolMap[1].upper }}
        </span>
      </kbd>
      <kbd @click="pushNumOrSymbol(symbolMap[2])" class="key">
        <span :class="{ key__inactive: isShiftPressed }">
          {{ symbolMap[2].lower }}
        </span>
        <span :class="{ key__inactive: !isShiftPressed }">
          {{ symbolMap[2].upper }}
        </span>
      </kbd>
      <kbd class="key function-key backspace" @click="$emit('backspace')">
        &larr;
      </kbd>
    </div>
    <div class="row first-row">
      <kbd class="key function-key tab" @click="$emit('keyStroke', '\t')">
        TAB &rarr;
      </kbd>
      <kbd
        class="key"
        @click="pushAlpha(item, 'first')"
        v-for="(item, index) in alphaMap('first')"
        :key="index"
      >
        <span
          :class="{
            key__inactive:
              (isCapsLock && !isShiftPressed) || (!isCapsLock && isShiftPressed)
          }"
        >
          {{ item.lower }}
        </span>
        <span
          :class="{
            key__inactive:
              (isCapsLock && isShiftPressed) || (!isCapsLock && !isShiftPressed)
          }"
        >
          {{ item.upper }}
        </span>
      </kbd>
      <kbd @click="pushNumOrSymbol(symbolMap[3])" class="key">
        <span :class="{ key__inactive: isShiftPressed }">
          {{ symbolMap[3].lower }}
        </span>
        <span :class="{ key__inactive: !isShiftPressed }">
          {{ symbolMap[3].upper }}
        </span>
      </kbd>
      <kbd @click="pushNumOrSymbol(symbolMap[4])" class="key">
        <span :class="{ key__inactive: isShiftPressed }">
          {{ symbolMap[4].lower }}
        </span>
        <span :class="{ key__inactive: !isShiftPressed }">
          {{ symbolMap[4].upper }}
        </span>
      </kbd>
      <kbd @click="pushNumOrSymbol(symbolMap[5])" class="key row-last-key">
        <span :class="{ key__inactive: isShiftPressed }">
          {{ symbolMap[5].lower }}
        </span>
        <span :class="{ key__inactive: !isShiftPressed }">
          {{ symbolMap[5].upper }}
        </span>
      </kbd>
    </div>
    <div class="row second-row">
      <kbd
        class="key function-key caps-lock"
        @click="isCapsLock = !isCapsLock"
        :class="{ active: isCapsLock }"
      >
        CAPS LOCK
        <span class="caps-lock__light"></span>
      </kbd>
      <kbd
        class="key"
        @click="pushAlpha(item, 'second')"
        v-for="(item, index) in alphaMap('second')"
        :key="index"
      >
        <span
          :class="{
            key__inactive:
              (isCapsLock && !isShiftPressed) || (!isCapsLock && isShiftPressed)
          }"
        >
          {{ item.lower }}
        </span>
        <span
          :class="{
            key__inactive:
              (isCapsLock && isShiftPressed) || (!isCapsLock && !isShiftPressed)
          }"
        >
          {{ item.upper }}
        </span>
      </kbd>
      <kbd @click="pushNumOrSymbol(symbolMap[6])" class="key">
        <span :class="{ key__inactive: isShiftPressed }">
          {{ symbolMap[6].lower }}
        </span>
        <span :class="{ key__inactive: !isShiftPressed }">
          {{ symbolMap[6].upper }}
        </span>
      </kbd>
      <kbd @click="pushNumOrSymbol(symbolMap[7])" class="key">
        <span :class="{ key__inactive: isShiftPressed }">
          {{ symbolMap[7].lower }}
        </span>
        <span :class="{ key__inactive: !isShiftPressed }">
          {{ symbolMap[7].upper }}
        </span>
      </kbd>
      <kbd class="key function-key return" @click="$emit('keyStroke', '\n')">
        RETURN
      </kbd>
    </div>
    <div class="row third-row">
      <kbd
        class="key function-key shift--left"
        @click="isShiftPressed = !isShiftPressed"
        :class="{ active: isShiftPressed }"
      >
        SHIFT &uarr;
      </kbd>
      <kbd
        class="key"
        @click="pushAlpha(item, 'third')"
        v-for="(item, index) in alphaMap('third')"
        :key="index"
      >
        <span
          :class="{
            key__inactive:
              (isCapsLock && !isShiftPressed) || (!isCapsLock && isShiftPressed)
          }"
        >
          {{ item.lower }}
        </span>
        <span
          :class="{
            key__inactive:
              (isCapsLock && isShiftPressed) || (!isCapsLock && !isShiftPressed)
          }"
        >
          {{ item.upper }}
        </span>
      </kbd>
      <kbd @click="pushNumOrSymbol(symbolMap[8])" class="key">
        <span :class="{ key__inactive: isShiftPressed }">
          {{ symbolMap[8].lower }}
        </span>
        <span :class="{ key__inactive: !isShiftPressed }">
          {{ symbolMap[8].upper }}
        </span>
      </kbd>
      <kbd @click="pushNumOrSymbol(symbolMap[9])" class="key">
        <span :class="{ key__inactive: isShiftPressed }">
          {{ symbolMap[9].lower }}
        </span>
        <span :class="{ key__inactive: !isShiftPressed }">
          {{ symbolMap[9].upper }}
        </span>
      </kbd>
      <kbd @click="pushNumOrSymbol(symbolMap[10])" class="key">
        <span :class="{ key__inactive: isShiftPressed }">
          {{ symbolMap[10].lower }}
        </span>
        <span :class="{ key__inactive: !isShiftPressed }">
          {{ symbolMap[10].upper }}
        </span>
      </kbd>
      <kbd
        class="key function-key shift--right"
        @click="isShiftPressed = !isShiftPressed"
        :class="{ active: isShiftPressed }"
      >
        SHIFT &uarr;</kbd
      >
    </div>
    <div class="row last-row">
      <kbd
        class="key function-key ctrl"
        @click="isCtrlPressed = !isCtrlPressed"
      >
        CTRL
      </kbd>
      <kbd class="key function-key space" @click="$emit('keyStroke', ' ')">
        SPACE
      </kbd>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      alphaRow: {
        first: 'QWERTYUIOP',
        second: 'ASDFGHJKL',
        third: 'ZXCVBNM'
      },
      numMap: [
        {
          lower: '1',
          upper: '!'
        },
        {
          lower: '2',
          upper: '@'
        },
        {
          lower: '3',
          upper: '#'
        },
        {
          lower: '4',
          upper: '$'
        },
        {
          lower: '5',
          upper: '%'
        },
        {
          lower: '6',
          upper: '^'
        },
        {
          lower: '7',
          upper: '&'
        },
        {
          lower: '8',
          upper: '*'
        },
        {
          lower: '9',
          upper: '('
        },
        {
          lower: '0',
          upper: ')'
        }
      ],
      symbolMap: [
        {
          lower: '`',
          upper: '~'
        },
        {
          lower: '-',
          upper: '_'
        },
        {
          lower: '=',
          upper: '+'
        },
        {
          lower: '[',
          upper: '{'
        },
        {
          lower: ']',
          upper: '}'
        },
        {
          lower: '\\',
          upper: '|'
        },
        {
          lower: ';',
          upper: ':'
        },
        {
          lower: "'",
          upper: '"'
        },
        {
          lower: ',',
          upper: '<'
        },
        {
          lower: '.',
          upper: '>'
        },
        {
          lower: '/',
          upper: '?'
        }
      ],
      isCapsLock: false,
      isShiftPressed: false,
      isCtrlPressed: false,
      randomizeKeys: true
    }
  },
  methods: {
    alphaMap(type) {
      return this.alphaRow[type]
        .split('')
        .map((el) => ({ lower: el.toLowerCase(), upper: el }))
    },
    pushNumOrSymbol(item, isNum) {
      this.$emit('keyStroke', this.isShiftPressed ? item.upper : item.lower)
      if (this.isShiftPressed) this.isShiftPressed = false
      if (this.randomizeKeys && isNum) {
        this.numMap = this.numMap.sort(() => 0.5 - Math.random())
      }
    },
    pushAlpha(item, type) {
      const val =
        (this.isCapsLock && !this.isShiftPressed) ||
        (!this.isCapsLock && this.isShiftPressed)
          ? item.upper
          : item.lower
      this.$emit('keyStroke', val)
      if (this.randomizeKeys)
        this.alphaRow[type] = this.alphaRow[type]
          .split('')
          .sort(() => 0.5 - Math.random())
          .join('')
      if (this.isShiftPressed) this.isShiftPressed = false
    }
  }
}
</script>

<style lang="scss">
.key-board {
  margin: 1rem;
  user-select: none;
  display: grid;
  grid-template-rows: repeat(5, 1fr);
  row-gap: 10px;

  .row {
    display: grid;
    grid-template-columns: repeat(15, 1fr);
    column-gap: 10px;

    .key {
      background-color: #eee;
      border-radius: 3px;
      border: 1px solid #b4b4b4;
      box-shadow: 0 1px 1px rgba(0, 0, 0, 0.2),
        0 2px 0 0 rgba(255, 255, 255, 0.7) inset;
      color: #333;
      font-size: 1.2rem;

      font-weight: 700;
      line-height: 1;
      padding: 2px 4px;
      white-space: nowrap;
      cursor: pointer;
      display: inline-flex;
      justify-content: center;
      align-items: center;
      position: relative;

      &:active {
        transform: translateY(2px);
      }

      &.backspace {
        font-size: 2rem;
        grid-column-end: span 2;
      }

      &.ctrl {
        grid-column-start: span 1;
      }

      &.space {
        grid-column: 6 / span 5;
      }

      &__inactive {
        position: absolute;
        top: 5px;
        left: 5px;
        font-size: 1rem;
        color: #888;
      }
    }

    &.first-row {
      grid-template-columns: repeat(30, 1fr);

      .key {
        grid-column: span 2;
        &.tab {
          grid-column-start: span 3;
        }
        &.row-last-key {
          grid-column: span 3;
        }
      }
    }

    &.second-row {
      grid-template-columns: repeat(45, 1fr);

      .key {
        grid-column: span 3;
        &.caps-lock {
          grid-column-start: span 5;

          .caps-lock__light {
            height: 10px;
            width: 10px;
            background: #999;
            border-radius: 50%;
            position: absolute;
            right: 5px;
            top: 5px;
          }

          &.active {
            .caps-lock__light {
              background: #00c500;
            }
          }
        }
        &.return {
          grid-column: span 7;
        }
      }
    }

    &.third-row {
      grid-template-columns: repeat(15, 1fr);
      .key {
        &.shift {
          &--left {
            grid-column-start: span 2;
            &.active {
              transform: translateY(2px);
            }
          }

          &--right {
            grid-column-end: span 3;
            &.active {
              transform: translateY(2px);
            }
          }
        }
      }
    }
  }
}
</style>
