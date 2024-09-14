<script>
    import { ModeWatcher } from 'mode-watcher';
    import Sidebar from '../Components/Sidebar.svelte';
    import '../app.css';
    import Button from '$lib/components/ui/button/button.svelte';
    import Icon from '@iconify/svelte';
    import MobileNav from '../Components/MobileNav.svelte';
</script>

<ModeWatcher />
<div class="flex">
    <Sidebar />
    <div class="p-5 absolute"><MobileNav /></div>
    <main class="flex-1 md:ml-64 min-w-[calc(100vw-16rem)]">
        <slot />
    </main>
</div>
