<template>
	<div id="app">
		<img alt="Vue logo" src="./assets/logo.png">
		<testForm />
	</div>
</template>

<script>
import testForm from './components/Form/Form.vue'

export default {
	name: 'App',
	components: {
		testForm
	}
}
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
body {
  background: #0D141F;
}
</style>
