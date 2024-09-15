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

<aside
    class="bg-muted/40 hidden border-r md:block overflow-hidden fixed left-0 top-0 h-full w-64"
>
    <div class="flex flex-col h-full">
        <div class="flex h-14 items-center border-b px-4 lg:h-[60px] lg:px-6">
            <a
                href="/"
                class="hover:text-primary transition-colors text-[13px] flex items-center font-semibold"
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
            <nav class="grid items-start px-2 text-lg font-medium lg:px-4">
                <a
                    href="timetable"
                    class="flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-all duration-200 hover:text-primary hover:scale-105"
                >
                    <Icon
                        icon="solar:calendar-bold"
                        class="w-5 h-5"
                    />
                    Rozvrh
                </a>
                <a
                    href="attendance"
                    class="flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-all duration-200 hover:text-primary hover:scale-105"
                >
                    <Icon
                        icon="mdi:user-clock-outline"
                        class="w-5 h-5"
                    />
                    Docházka
                </a>
                <a
                    href="classification"
                    class="flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-all duration-200 hover:text-primary hover:scale-105"
                >
                    <Icon
                        icon="mdi:report-line-variant"
                        class="w-5 h-5"
                    />
                    Klasifikace
                </a>
                <a
                    href="work"
                    class="flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-all duration-200 hover:text-primary hover:scale-105"
                >
                    <Icon
                        icon="mdi:work-outline"
                        class="w-5 h-5"
                    />
                    Práce
                </a>
                <a
                    href="finance"
                    class="flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-all duration-200 hover:text-primary hover:scale-105"
                >
                    <Icon
                        icon="mdi:attach-money"
                        class="w-5 h-5"
                    />
                    Finance
                </a>
                <a
                    href="tests"
                    class="flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-all duration-200 hover:text-primary hover:scale-105"
                >
                    <Icon
                        icon="mdi:file-document-outline"
                        class="w-5 h-5"
                    />
                    Dokumenty
                </a>
                <a
                    href="tests"
                    class="flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-all duration-200 hover:text-primary hover:scale-105"
                >
                    <Icon
                        icon="material-symbols:link"
                        class="w-5 h-5"
                    />
                    Odkazy
                </a>
                <a
                    href="tests"
                    class="flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-all duration-200 hover:text-primary hover:scale-105"
                >
                    <Icon
                        icon="mdi:vote-outline"
                        class="w-5 h-5"
                    />
                    Volby
                </a>
                <a
                    href="tests"
                    class="flex items-center gap-3 rounded-lg px-3 py-2 text-muted-foreground transition-all duration-200 hover:text-primary hover:scale-105"
                >
                    <Icon
                        icon="ph:exam"
                        class="w-5 h-5"
                    />
                    Zkoušky
                </a>
            </nav>
        </div>
        <div class="p-2 lg:p-4">
            <a
                href="profile"
                class="font-medium text-lg flex items-center gap-3 rounded-lg px-3 text-muted-foreground transition-all duration-200 hover:text-primary hover:scale-105"
            >
                <div class="rounded-full bg-[#fa334b] w-7 h-7"></div>
                Profil
            </a>
        </div>
    </div>
</aside>

<style>
</style>
