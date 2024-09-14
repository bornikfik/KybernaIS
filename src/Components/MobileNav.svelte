<script lang="ts">
    import Button from '$lib/components/ui/button/button.svelte';
    import * as Sheet from '$lib/components/ui/sheet';
    import Icon from '@iconify/svelte';
</script>

<Sheet.Root>
    <Sheet.Trigger>
        <Button
            variant="outline"
            size="icon"
            class="shrink-0 md:hidden"
        >
            <Icon icon="mdi:menu" />
            <span class="sr-only">Toggle nav menu</span>
        </Button>
    </Sheet.Trigger>
    <Sheet.Content
        side="left"
        class="flex flex-col"
    >
        <nav class="grid gap-2 text-lg font-medium w-fit">
            <a
                href="/"
                class="flex items-center gap-2 text-lg font-semibold"
            >
                <span>Kyberna Informační Systém</span>
            </a>
            <a
                href="timetable"
                class="mx-[-0.65rem] flex items-center gap-4 rounded-xl px-3 py-2 text-muted-foreground hover:text-foreground"
            >
                <Icon
                    icon="solar:calendar-bold"
                    class="w-5 h-5"
                />
                Rozvrh
            </a>
            <a
                href="attendance"
                class="mx-[-0.65rem] flex items-center gap-4 rounded-xl px-3 py-2 text-muted-foreground hover:text-foreground"
            >
                <Icon
                    icon="mdi:user-clock-outline"
                    class="w-5 h-5"
                />
                Docházka
            </a>
            <a
                href="classification"
                class="mx-[-0.65rem] flex items-center gap-4 rounded-xl px-3 py-2 text-muted-foreground hover:text-foreground"
            >
                <Icon
                    icon="mdi:report-line-variant"
                    class="w-5 h-5"
                />
                Klasifikace
            </a>
            <a
                href="work"
                class="mx-[-0.65rem] flex items-center gap-4 rounded-xl px-3 py-2 text-muted-foreground hover:text-foreground"
            >
                <Icon
                    icon="mdi:work-outline"
                    class="w-5 h-5"
                />
                Práce
            </a>
            <a
                href="finance"
                class="mx-[-0.65rem] flex items-center gap-4 rounded-xl px-3 py-2 text-muted-foreground hover:text-foreground"
            >
                <Icon
                    icon="mdi:attach-money"
                    class="w-5 h-5"
                />
                Finance
            </a>
        </nav>
        <div class="mt-auto w-fit">
            <a
                href="tests"
                class="mx-[-0.65rem] flex items-center gap-4 rounded-xl px-3 py-2 text-muted-foreground hover:text-foreground"
            >
                <Icon
                    icon="ph:exam"
                    class="w-5 h-5"
                />
                Zkoušky
            </a>
            <a
                href="documents"
                class="mx-[-0.65rem] flex items-center gap-4 rounded-xl px-3 py-2 text-muted-foreground hover:text-foreground"
            >
                <Icon
                    icon="mdi:file-document-outline"
                    class="w-5 h-5"
                />
                Dokumenty
            </a>
            <a
                href="links"
                class="mx-[-0.65rem] flex items-center gap-4 rounded-xl px-3 py-2 text-muted-foreground hover:text-foreground"
            >
                <Icon
                    icon="material-symbols:link"
                    class="w-5 h-5"
                />
                Odkazy
            </a>
            <a
                href="votes"
                class="mx-[-0.65rem] flex items-center gap-4 rounded-xl px-3 py-2 text-muted-foreground hover:text-foreground"
            >
                <Icon
                    icon="mdi:vote-outline"
                    class="w-5 h-5"
                />
                Volby
            </a>
            <a
                href="logout"
                class="mx-[-0.65rem] flex items-center gap-4 rounded-xl px-3 py-2 text-muted-foreground hover:text-foreground"
            >
                <Icon
                    icon="material-symbols:logout"
                    class="w-5 h-5"
                />
                Odhlásit se
            </a>
        </div>
    </Sheet.Content>
</Sheet.Root>
