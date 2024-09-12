<script>
    import { Button } from '$lib/components/ui/button';
    import Icon from '@iconify/svelte';
    import { fade } from 'svelte/transition';

    let isNotificationOn = true;
    let isButtonDisabled = false;

    function toggleNotification() {
        if (!isButtonDisabled) {
            isNotificationOn = !isNotificationOn;
            isButtonDisabled = true;

            setTimeout(() => {
                isButtonDisabled = false;
            }, 500);
        }
    }
</script>

<div
    class="bg-muted/40 hidden border-r md:block overflow-hidden fixed left-0 top-0 h-full w-64"
>
    <div class="flex flex-col h-full">
        <div class="flex h-14 items-center border-b px-4 lg:h-[60px] lg:px-6">
            <a
                href="/"
                class="hover:text-muted-foreground transition-colors text-[15px] flex items-center font-semibold"
            >
                <span>Kyberna Informační Systém</span>
            </a>
            <Button
                variant="outline"
                size="icon"
                class="ml-auto h-8 w-8"
                on:click={toggleNotification}
                disabled={isButtonDisabled}
            >
                {#if isNotificationOn}
                    <div in:fade={{ duration: 150 }}>
                        <Icon icon="mdi:bell-outline" />
                    </div>
                {:else}
                    <div in:fade={{ duration: 150 }}>
                        <Icon icon="mdi:bell-off-outline" />
                    </div>
                {/if}
                <span class="sr-only">Toggle Notifications</span>
            </Button>
        </div>
        <div class="flex-1 overflow-y-auto">
            <nav class="grid items-start px-2 text-sm font-medium lg:px-4">
                <a
                    href="timetable"
                    class="text-lg flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-colors hover:text-primary"
                >
                    <Icon
                        icon="solar:calendar-bold"
                        class="w-6 h-6"
                    />
                    Rozvrh
                </a>
                <a
                    href="attendance"
                    class="text-lg flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-colors hover:text-primary"
                >
                    <Icon
                        icon="mdi:user-clock-outline"
                        class="w-6 h-6"
                    />
                    Docházka
                </a>
                <a
                    href="classification"
                    class="text-lg flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-colors hover:text-primary"
                >
                    <Icon
                        icon="mdi:report-line-variant"
                        class="w-6 h-6"
                    />
                    Klasifikace
                </a>
                <a
                    href="work"
                    class="text-lg flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-colors hover:text-primary"
                >
                    <Icon
                        icon="mdi:work-outline"
                        class="w-6 h-6"
                    />
                    Práce
                </a>
                <a
                    href="finance"
                    class="text-lg flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-colors hover:text-primary"
                >
                    <Icon
                        icon="mdi:attach-money"
                        class="w-6 h-6"
                    />
                    Finance
                </a>
            </nav>
        </div>
        <nav class="grid items-start px-2 text-sm font-medium lg:px-4 pb-4">
            <div>
                <a
                    href="tests"
                    class="text-lg flex items-center gap-3 rounded-lg px-3 pb-2 text-muted-foreground transition-colors hover:text-primary"
                >
                    <Icon
                        icon="ph:exam"
                        class="w-6 h-6"
                    />
                    Zkoušky
                </a>
                <a
                    href="documents"
                    class="text-lg flex items-center gap-3 rounded-lg px-3 pb-2 text-muted-foreground transition-colors hover:text-primary"
                >
                    <Icon
                        icon="mdi:file-document-outline"
                        class="w-6 h-6"
                    />
                    Dokumenty
                </a>
                <a
                    href="links"
                    class="text-lg flex items-center gap-3 rounded-lg px-3 pb-2 text-muted-foreground transition-colors hover:text-primary"
                >
                    <Icon
                        icon="material-symbols:link"
                        class="w-6 h-6"
                    />
                    Odkazy
                </a>
                <a
                    href="votes"
                    class="text-lg flex items-center gap-3 rounded-lg px-3 pb-2 text-muted-foreground transition-colors hover:text-primary"
                >
                    <Icon
                        icon="mdi:vote-outline"
                        class="w-6 h-6"
                    />
                    Volby
                </a>
                <a
                    href="logout"
                    class="text-lg flex items-center gap-3 rounded-lg px-3 text-muted-foreground transition-colors hover:text-primary"
                >
                    <Icon
                        icon="material-symbols:logout"
                        class="w-6 h-6"
                    />
                    Odhlásit se
                </a>
            </div>
        </nav>
    </div>
</div>
