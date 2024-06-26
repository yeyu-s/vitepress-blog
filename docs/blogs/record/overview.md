# Markdown Extension Examples


This page demonstrates some of the built-in markdown extensions provided by VitePress.

## Syntax Highlighting

::: details
This is a details block.
:::

<script setup>
import { ref } from 'vue'

const count = ref(0)
</script>

## Markdown Content

The count is: {{ count }}

<button :class="$style.button" @click="count++">Increment</button>

<style module>
.button {
  color: red;
  font-weight: bold;
}
</style>