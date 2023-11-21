<template>
	<div id="app">
		<img alt="Vue logo" src="./assets/logo.png">
		<HelloWorld msg="Welcome to Your Vue.js App" />
		<testForm />
	</div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import testForm from './components/Form/Form.vue'

export default {
	name: 'App',
	components: {
		HelloWorld,
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
</style>
