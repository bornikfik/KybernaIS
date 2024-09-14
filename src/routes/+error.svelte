<script lang="ts">
    import { goto } from '$app/navigation';
    import { page } from '$app/stores';
    import Button from '$lib/components/ui/button/button.svelte';
</script>

<div class="min-h-screen flex items-center justify-center flex-col gap-4">
    <h1 class="text-9xl text-red-500">{$page.status}</h1>
    <h3 class="text-2xl">{$page.error?.message}</h3>
    <Button
        variant="outline"
        on:click={() => goto('/')}
        size="lg">Return back</Button
    >
</div>
