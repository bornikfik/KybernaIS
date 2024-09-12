<script>
    import { ModeWatcher } from 'mode-watcher';
    import Sidebar from '../Components/Sidebar.svelte';
    import '../app.css';
</script>

<Sidebar />
<ModeWatcher />
<slot></slot>
