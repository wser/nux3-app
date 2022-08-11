# Middleware

There are three kinds of route middleware:

1. Anonymous route middleware, which are defined directly in the pages where they are used.
2. Named route middleware, which are placed in the middleware/ directory and will be automatically loaded via asynchronous import when used on a page.
3. Global route middleware, which are placed in the middleware/ directory (with a .global suffix) and will be automatically run on every route change.

## Middleware Example

Test out named middleware in the following example! Without entering your user name, you will be blocked from visiting the private page.

::CodeBlock{componentName="MiddlewareDemo"}
#tab1
/middleware/auth.ts
#code1

```ts
export default defineNuxtRouteMiddleware((to, from) => {
	const username = useState('username');

	if (!username.value) {
		process.client && alert('Sorry, you need to fill your username');
		return navigateTo('/');
	}
});
```

#tab2
/pages/private.vue
#code2

```vue
<script setup>
	definePageMeta({
		middleware: 'auth'
	});
	const username = useState('username');
</script>

<template>
	<div>
		<h1>Welcome {{ username }}</h1>
		<NuxtLink to="/">Home</NuxtLink>
	</div>
</template>
```

#tab3
/pages/indev.vue
#code3

```vue
<script setup>
	const username = useState('username');
</script>

<template>
	<div>
		<h1>Home</h1>
		<p>In order to enter the secret page, you need to fill your username:</p>
		<p><input v-model="username" placeholder="Username" /></p>
		<NuxtLink to="/secret">Secret page</NuxtLink>
	</div>
</template>
```

#tab4
Result
::