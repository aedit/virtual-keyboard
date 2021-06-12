<template>
  <div ref="key-board" class="key-board">
    <div class="row num-row">
      <kbd class="key">
        {{ symbolMap[0].lower }}
        {{ symbolMap[0].upper }}
      </kbd>
      <kbd class="key" v-for="(item, index) in numMap" :key="index">
        {{ item.lower }}
        {{ item.upper }}
      </kbd>
      <kbd class="key">
        {{ symbolMap[1].lower }}
        {{ symbolMap[1].upper }}
      </kbd>
      <kbd class="key">
        {{ symbolMap[2].lower }}
        {{ symbolMap[2].upper }}
      </kbd>
      <kbd class="key function-key backspace">&larr;</kbd>
    </div>
    <div class="row first-row">
      <kbd class="key function-key tab">TAB &rarr;</kbd>
      <kbd
        class="key"
        v-for="(item, index) in alphaMap(alphaFirst)"
        :key="index"
      >
        {{ item.lower }}
        {{ item.upper }}
      </kbd>
      <kbd class="key">
        {{ symbolMap[3].lower }}
        {{ symbolMap[3].upper }}
      </kbd>
      <kbd class="key">
        {{ symbolMap[4].lower }}
        {{ symbolMap[4].upper }}
      </kbd>
      <kbd class="key row-last-key">
        {{ symbolMap[5].lower }}
        {{ symbolMap[5].upper }}
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
        v-for="(item, index) in alphaMap(alphaSecond)"
        :key="index"
      >
        {{ item.lower }}
        {{ item.upper }}
      </kbd>
      <kbd class="key">
        {{ symbolMap[6].lower }}
        {{ symbolMap[6].upper }}
      </kbd>
      <kbd class="key">
        {{ symbolMap[7].lower }}
        {{ symbolMap[7].upper }}
      </kbd>
      <kbd class="key function-key return">RETURN</kbd>
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
        v-for="(item, index) in alphaMap(alphaThird)"
        :key="index"
      >
        {{ item.lower }}
        {{ item.upper }}
      </kbd>
      <kbd class="key">
        {{ symbolMap[8].lower }}
        {{ symbolMap[8].upper }}
      </kbd>
      <kbd class="key">
        {{ symbolMap[9].lower }}
        {{ symbolMap[9].upper }}
      </kbd>
      <kbd class="key">
        {{ symbolMap[10].lower }}
        {{ symbolMap[10].upper }}
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
      <kbd class="key function-key space">SPACE</kbd>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      alphaFirst: 'QWERTYUIOP',
      alphaSecond: 'ASDFGHJKL',
      alphaThird: 'ZXCVBNM',
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
      isShiftPressed: false
    }
  },
  methods: {
    alphaMap(alphaRow = '') {
      return alphaRow
        .split('')
        .map((el) => ({ lower: el.toLowerCase(), upper: el }))
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

      &:active {
        transform: translateY(2px);
      }

      &.backspace {
        font-size: 2rem;
        grid-column-end: span 2;
      }

      &.space {
        grid-column: 6 / span 5;
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
          position: relative;

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
