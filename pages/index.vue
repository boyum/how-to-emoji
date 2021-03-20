<template>
  <section class="container">
    <h1 class="title">
      Hi! We're guessing that you're using {{ os.family }} {{ os.version }}! 🎆
    </h1>
    <h2
      v-if="currentCombination.keys || currentCombination.alternative"
      class="subtitle"
    >
      This is how you can type emoji on {{ currentDevice }}:
    </h2>
    <div
      v-if="currentCombination.keys || currentCombination.alternative"
      class="howto"
    >
      <div
        v-if="currentCombination.keys"
        class="keys"
      >
        <span
          v-for="(key, index) in currentCombination.keys"
          :key="index"
        >
          <span v-if="index > 0"> + </span><kbd>{{ key }}</kbd>
        </span>
      </div>
      <div
        v-if="!currentCombination.keys && currentCombination.alternative"
        class="alternative"
      >
        {{ currentCombination.alternative }}
      </div>
    </div>
    <h2
      v-if="!currentCombination.keys && !currentCombination.alternative"
      class="subtitle"
    >
      We don't know how to type emojis on your device! Please help us on
      <a href="https://github.com/boyum/how-to-emoji">GitHub</a>
    </h2>
    <nav class="other-combinations">
      <h2>Click to check other devices:</h2>
      <ul>
        <li
          v-for="(c, index) in combinations"
          :key="index"
        >
          <button
            type="button"
            @click="setCombination(index)"
          >
            {{ c.label }}
          </button>
        </li>
      </ul>
    </nav>
  </section>
</template>

<script>
import { os, product } from "platform";

const combinations = [
  {
    label: "Windows 10",
    osFamily: "Windows",
    osVersion: "10",
    keys: ["⊞ Win", "."]
  },
  {
    label: "Android",
    osFamily: "Android",
    alternative:
      "Find the emoji icon next to the letters on your on-screen keyboard"
  },
  {
    label: "iOS",
    osFamily: "iOS",
    alternative:
      "Find the emoji icon next to the letters on your on-screen keyboard"
  },
  {
    label: "macOS",
    osFamily: "OS X",
    keys: ["⌘ Cmd", "⌃ Ctrl", "Space"]
  }
];

const currentCombination = getCombination(os.family, os.version);

function getCombination(family, version) {
  family = family?.toLowerCase() ?? "";
  version = version?.toLowerCase() ?? "";

  return (
    combinations.find(combination => {
      const isCorrectFamily = combination.osFamily?.toLowerCase() === family;
      const isCorrectVersion = combination.osVersion
        ? combination.osVersion.toLowerCase() === version
        : true;

      return isCorrectFamily && isCorrectVersion;
    }) ?? {}
  );
}

export default {
  components: {},
  data() {
    return {
      os,
      product,
      currentCombination,
      combination: currentCombination,
      combinations,
      currentDevice: "your device"
    };
  },
  methods: {
    setCombination(index) {
      this.currentCombination = combinations[index];
      this.currentDevice = combinations[index].label;
    }
  }
};
</script>

<style>
.container {
  align-items: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin: 0 auto;
  max-width: 700px;
  min-height: 100vh;
  text-align: center;
  width: 90%;
}

.title {
  color: #35495e;
  display: block;
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  font-size: 3.5rem;
  font-weight: 300;
  letter-spacing: 1px;
  margin-bottom: 2rem;
}
.subtitle {
  margin-bottom: 1rem;
}

h2 {
  color: #526488;
  font-size: 2rem;
  font-weight: 300;
  padding-bottom: 15px;
  word-spacing: 5px;
}

.links {
  padding-top: 15px;
}

.howto {
  margin-bottom: 4rem;
}

.alternative {
  background-color: #f2f2f2;
  font-weight: 300;
  font-size: 2rem;
  padding: 2rem 3rem;
}

kbd {
  border: 1px solid;
  border-bottom: 3px solid;
  border-radius: 5px;
  padding: 0.3em;
}

.other-combinations ul {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  list-style-type: none;
  margin: 0;
  padding: 0;
}

.other-combinations button {
  background: #fff;
  border-radius: 5px;
  border: 1px solid;
  cursor: pointer;
  display: inline-block;
  font-family: inherit;
  font-size: 1rem;
  padding: 0.3em;
}

.other-combinations li {
  margin-bottom: 0.5em;
}

.other-combinations li + li {
  margin-left: 0.5em;
}
</style>
