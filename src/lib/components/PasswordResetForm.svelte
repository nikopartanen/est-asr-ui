<script>
	import Input from '$lib/components/Input.svelte';
	import Button from '$lib/components/Button.svelte';
	import { _ } from 'svelte-i18n';
	import { createEventDispatcher } from 'svelte';

	let password = '';
	let confirmPassword = '';
	let error;
	let confirmPasswordInputRef;

	const dispatch = createEventDispatcher();

	function submit() {
		error = null;
		if (password !== confirmPassword) {
			error = $_('passwordReset.passwordsDontMatch');
			confirmPasswordInputRef.focus();
			return;
		}

		dispatch('submit', {
			password
		});
	}
</script>

<form on:submit|preventDefault={submit} class="space-y-5 {$$props.class}">
	<Input
		label={$_('passwordReset.password')}
		id="password"
		name="password"
		type="password"
		bind:value={password}
	/>
	<Input
		label={$_('passwordReset.passwordConfirm')}
		id="confirm-password"
		name="confirm-password"
		type="password"
		bind:value={confirmPassword}
		bind:inputRef={confirmPasswordInputRef}
	/>
	{#if error}
		<p class="text-red-600 text-sm font-semibold">{error}</p>
	{/if}
	<Button type="submit">{$_('passwordReset.change')}</Button>
</form>
