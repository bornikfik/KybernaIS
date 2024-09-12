<script lang="ts">
    import { Button } from '$lib/components/ui/button';
    import { Input } from '$lib/components/ui/input';
    import { Label } from '$lib/components/ui/label';
    import { Switch } from '$lib/components/ui/switch';

    const days = ['Pondělí', 'Úterý', 'Středa', 'Čtvrtek', 'Pátek'] as const;
    const timeSlots = [
        '0. 7:00-7:45',
        '1. 7:50-8:35',
        '2. 8:45-9:30',
        '3. 9:45-10:30',
        '4. 10:45-11:30',
        '5. 11:45-12:30',
        '6. 12:45-13:30',
        '7. 13:45-14:30',
    ] as const;

    type Day = (typeof days)[number];
    type TimeSlot = (typeof timeSlots)[number];

    type LessonInfo = {
        subject: string;
        classroom: string;
        teacher: string;
        meetLink: string;
    };

    const timetableData: Record<Day, Partial<Record<TimeSlot, LessonInfo>>> = {
        Pondělí: {
            '1. 7:50-8:35': {
                subject: 'Anglický Jazyk',
                classroom: 'A101',
                teacher: 'Mgr. Nováková',
                meetLink: 'https://meet.google.com/abc-defg-hij',
            },
            '3. 9:45-10:30': {
                subject: 'Matematika',
                classroom: 'B202',
                teacher: 'Mgr. Svoboda',
                meetLink: 'https://meet.google.com/klm-nop-qrs',
            },
            '6. 12:45-13:30': {
                subject: 'Chemie',
                classroom: 'C303',
                teacher: 'Ing. Procházka',
                meetLink: 'https://meet.google.com/tuv-wxy-z12',
            },
        },
        Úterý: {},
        Středa: {
            '4. 10:45-11:30': {
                subject: 'Biologie',
                classroom: 'D404',
                teacher: 'RNDr. Kučerová',
                meetLink: 'https://meet.google.com/345-678-901',
            },
            '6. 12:45-13:30': {
                subject: 'Anglický Jazyk',
                classroom: 'A101',
                teacher: 'Mgr. Nováková',
                meetLink: 'https://meet.google.com/abc-defg-hij',
            },
        },
        Čtvrtek: {},
        Pátek: {
            '3. 9:45-10:30': {
                subject: 'Dějepis',
                classroom: 'E505',
                teacher: 'PhDr. Dvořák',
                meetLink: 'https://meet.google.com/234-567-890',
            },
            '5. 11:45-12:30': {
                subject: 'Výtvarná Výchova',
                classroom: 'F606',
                teacher: 'Mgr. Malá',
                meetLink: 'https://meet.google.com/123-456-789',
            },
            '7. 13:45-14:30': {
                subject: 'Tělesná Výchova',
                classroom: 'Tělocvična',
                teacher: 'Mgr. Veselý',
                meetLink: 'https://meet.google.com/987-654-321',
            },
        },
    };

    let isCurrentTimetable = false;
    let selectedDate = new Date().toISOString().split('T')[0];

    function toggleTimetable() {
        isCurrentTimetable = !isCurrentTimetable;
    }

    $: displayedTimetable =
        isCurrentTimetable ? getCurrentTimetable(selectedDate) : timetableData;

    function getCurrentTimetable(date: string) {
        // Zde by byla logika pro získání aktuálního rozvrhu podle data
        // Pro tento příklad vrátíme stejný rozvrh
        return timetableData;
    }
</script>

<svelte:head>
    <link
        href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap"
        rel="stylesheet"
    />
</svelte:head>

<div
    class="w-full max-w-4xl mx-auto p-4 bg-background min-h-screen font-poppins"
>
    <h1 class="text-3xl font-bold text-center mb-6 text-primary">
        Školní Rozvrh
    </h1>

    <div class="flex justify-between items-center mb-4">
        <div class="flex items-center space-x-2">
            <Switch
                id="timetable-switch"
                checked={isCurrentTimetable}
                onCheckedChange={toggleTimetable}
            />
            <Label for="timetable-switch">
                {isCurrentTimetable ? 'Aktuální rozvrh' : 'Stálý rozvrh'}
            </Label>
        </div>
        <div class="flex items-center space-x-2">
            <div class:opacity-50={!isCurrentTimetable}>
                <Label for="date-input">Datum:</Label>
            </div>
            <div class:opacity-50={!isCurrentTimetable}>
                <Input
                    type="date"
                    id="date-input"
                    bind:value={selectedDate}
                    disabled={!isCurrentTimetable}
                />
            </div>
        </div>
    </div>

    <div
        class="grid grid-cols-11 grid-rows-8 overflow-hidden rounded-lg shadow-md bg-background text-sm"
    >
        <div
            class="border p-2 flex items-center justify-center text-center bg-muted text-muted-foreground font-semibold"
        >
            Čas
        </div>
        {#each days as day}
            <div
                class="border p-2 text-center col-span-2 bg-muted text-muted-foreground font-semibold flex items-center justify-center"
            >
                {day}
            </div>
        {/each}
        {#each timeSlots as tslot}
            <div
                class="border p-2 text-center bg-muted text-muted-foreground font-medium"
            >
                {tslot}
            </div>
            {#each days as day}
                <div class="border p-1 text-center col-span-2">
                    {#if displayedTimetable[day]?.[tslot]}
                        <a
                            href={displayedTimetable[day][tslot].meetLink}
                            target="_blank"
                            rel="noopener noreferrer"
                            class="block bg-accent rounded-lg p-2 shadow-sm transition-all hover:shadow-md hover:bg-accent-foreground hover:text-accent cursor-pointer"
                        >
                            <p
                                class="text-lg font-semibold text-accent-foreground"
                            >
                                {displayedTimetable[day][tslot].subject}
                            </p>
                            <p class="text-xs">
                                {displayedTimetable[day][tslot].classroom}
                            </p>
                            <p class="text-xs">
                                {displayedTimetable[day][tslot].teacher}
                            </p>
                        </a>
                    {/if}
                </div>
            {/each}
        {/each}
    </div>
</div>
