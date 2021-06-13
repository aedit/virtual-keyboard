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
        class="key function-key ctrl--left"
        @click="isCtrlPressed = !isCtrlPressed"
        :class="{ active: isCtrlPressed }"
      >
        CTRL
      </kbd>
      <kbd class="key function-key space" @click="$emit('keyStroke', ' ')">
        SPACE
      </kbd>
      <kbd
        class="key function-key ctrl--right"
        @click="isCtrlPressed = !isCtrlPressed"
        :class="{ active: isCtrlPressed }"
      >
        CTRL
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
      randomizeKeys: false
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
