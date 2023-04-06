<!-- eslint-disable vue/multi-word-component-names -->

<template>
  <div>
    <slot />
  </div>
</template>

<style>
html {
  font-family: "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI",
    Roboto, "Helvetica Neue", Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

.button--green {
  display: inline-block;
  border-radius: 0.25rem;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 0.625rem 1.875rem;
}

.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}

.button--grey {
  border-radius: 0.25rem;
  border: 1px solid #35495e;
  color: #35495e;
  display: inline-block;
  margin-left: 0.9375rem;
  padding: 0.625rem 1.875rem;
  text-decoration: none;
}

.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}
</style>
