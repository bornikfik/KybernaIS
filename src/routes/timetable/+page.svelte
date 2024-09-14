<script lang="ts">
    import { Button } from '$lib/components/ui/button';
    import { Input } from '$lib/components/ui/input';
    import { Label } from '$lib/components/ui/label';
    import { Switch } from '$lib/components/ui/switch';
    import { onMount } from 'svelte';

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

    let isCurrentTimetable = true;
    let selectedDate = new Date().toISOString().split('T')[0];
    let isToggleCooldown = false;

    function toggleTimetable() {
        if (!isToggleCooldown) {
            isToggleCooldown = true;
            setTimeout(() => {
                isCurrentTimetable = !isCurrentTimetable;
                isToggleCooldown = false;
            }, 150);
        }
    }

    $: displayedTimetable =
        isCurrentTimetable ? getCurrentTimetable(selectedDate) : timetableData;

    let ct: {};
    onMount(async () => {
        let res = await fetch(
            'https://sis.ssakhk.cz/api/v1/getTimeTableByUserId',
            {
                method: 'POST',
                headers: {
                    'Content-type': 'application/json',
                    'User-Agent': 'insomnia/9.3.3',
                },
                body: JSON.stringify({
                    userid: 12000,
                    dateTime: selectedDate,
                }),
            }
        );

        ct = await res.json();
    });

    async function getCurrentTimetable(date: string) {
        return ct;
    }
</script>

<!-- <button aria-label="Refresh">Refresh table</button> -->

<div
    class="w-full max-w-6xl mx-auto p-6 bg-background min-h-screen font-poppins flex flex-col justify-center"
>
    <div>
        <h1 class="text-4xl font-bold text-center mb-8 text-primary">
            Školní Rozvrh
        </h1>

        <div
            class="flex justify-between items-center mb-8 bg-secondary rounded-lg p-5 shadow-md"
        >
            <div class="flex items-center space-x-5">
                <Switch
                    id="timetable-switch"
                    checked={isCurrentTimetable}
                    onCheckedChange={toggleTimetable}
                    disabled={isToggleCooldown}
                />
                <div class="text-base font-medium">
                    <Label for="timetable-switch">
                        {isCurrentTimetable ? 'Aktuální rozvrh' : (
                            'Stálý rozvrh'
                        )}
                    </Label>
                </div>
            </div>
            <div class="flex items-center space-x-5">
                <div
                    class="text-base font-medium"
                    class:opacity-50={!isCurrentTimetable}
                >
                    <Label for="date-input">Datum:</Label>
                </div>
                <div class:opacity-50={!isCurrentTimetable}>
                    <Input
                        type="date"
                        id="date-input"
                        bind:value={selectedDate}
                        disabled={!isCurrentTimetable}
                        class="w-48"
                    />
                </div>
            </div>
        </div>

        <div
            class="grid grid-cols-11 grid-rows-8 overflow-hidden rounded-lg shadow-lg bg-background text-sm"
        >
            <div
                class="border-r border-b border-r-background border-b-background p-2 flex items-center justify-center text-center bg-muted text-muted-foreground font-semibold"
            >
                Čas
            </div>
            {#each days as day}
                <div
                    class="border-x border-x-background p-2 text-center col-span-2 bg-muted text-muted-foreground font-semibold flex items-center justify-center"
                >
                    {day}
                </div>
            {/each}
            {#each timeSlots as tslot}
                <div
                    class="border-y border-y-background p-1 text-center bg-muted text-muted-foreground font-medium whitespace-nowrap overflow-hidden text-ellipsis flex items-center justify-center"
                >
                    {tslot.split(' ')[1]}
                </div>
                {#each days as day}
                    <div class="border p-1 text-center col-span-2 h-[74px]">
                        {#if displayedTimetable[day]?.[tslot]}
                            <a
                                href={displayedTimetable[day][tslot].meetLink}
                                target="_blank"
                                rel="noopener noreferrer"
                                class="bg-accent text-accent-foreground rounded p-1 shadow-sm transition-all hover:bg-accent-foreground hover:text-accent cursor-pointer h-full flex flex-col justify-between"
                            >
                                <p
                                    class="text-base font-semibold whitespace-nowrap overflow-hidden text-ellipsis"
                                >
                                    {displayedTimetable[day][tslot].subject}
                                </p>
                                <div>
                                    <p
                                        class="text-xs whitespace-nowrap overflow-hidden text-ellipsis"
                                    >
                                        {displayedTimetable[day][tslot]
                                            .classroom}
                                    </p>
                                    <p
                                        class="text-xs whitespace-nowrap overflow-hidden text-ellipsis"
                                    >
                                        {displayedTimetable[day][tslot].teacher}
                                    </p>
                                </div>
                            </a>
                        {/if}
                    </div>
                {/each}
            {/each}
        </div>
    </div>
</div>
