<script lang="ts">
    import { Calendar } from 'lucide-svelte';
    import { Switch } from '$lib/components/ui/switch';
    import {
        Table,
        TableBody,
        TableCell,
        TableHead,
        TableHeader,
        TableRow,
    } from '$lib/components/ui/table';

    let permanentSchedule = true;
    let currentDate = '2024-09-14';

    const timeSlots = [
        '7:00-7:45',
        '7:50-8:35',
        '8:45-9:30',
        '9:45-10:30',
        '10:45-11:30',
        '11:45-12:30',
        '12:45-13:30',
        '13:45-14:30',
    ];

    const days = ['Pondělí', 'Úterý', 'Středa', 'Čtvrtek', 'Pátek'];

    const schedule = {
        Pondělí: {
            '7:50-8:35': {
                subject: 'Anglický Jazyk',
                room: 'A101',
                teacher: 'Mgr. Nováková',
            },
            '9:45-10:30': {
                subject: 'Matematika',
                room: 'B202',
                teacher: 'Mgr. Svoboda',
            },
            '12:45-13:30': {
                subject: 'Chemie',
                room: 'C303',
                teacher: 'Ing. Procházka',
            },
        },
        Středa: {
            '10:45-11:30': {
                subject: 'Biologie',
                room: 'D404',
                teacher: 'RNDr. Kučerová',
            },
            '12:45-13:30': {
                subject: 'Anglický Jazyk',
                room: 'A101',
                teacher: 'Mgr. Nováková',
            },
        },
        Pátek: {
            '9:45-10:30': {
                subject: 'Dějepis',
                room: 'E505',
                teacher: 'PhDr. Dvořák',
            },
            '11:45-12:30': {
                subject: 'Výtvarná Výchova',
                room: 'F606',
                teacher: 'Mgr. Malá',
            },
            '13:45-14:30': {
                subject: 'Tělesná Výchova',
                room: 'Tělocvična',
                teacher: 'Mgr. Veselý',
            },
        },
    };
</script>

<div class="flex justify-center items-center min-h-screen bg-background p-4">
    <div
        class="container bg-muted/40 rounded-lg shadow-lg text-slate-100 p-6 max-w-7xl"
    >
        <h1 class="text-2xl font-bold mb-4">Školní Rozvrh</h1>

        <div
            class="flex justify-between items-center mb-4 bg-slate-800 p-3 rounded-lg"
        >
            <div class="flex items-center space-x-3">
                <Switch bind:checked={permanentSchedule} />
                <label
                    for="permanent-schedule"
                    class="text-sm font-medium"
                >
                    Stálý rozvrh
                </label>
            </div>

            <div class="flex items-center space-x-3">
                <Calendar class="h-5 w-5 text-slate-400" />
                <input
                    type="date"
                    bind:value={currentDate}
                    class="bg-slate-700 text-slate-100 rounded-md border border-slate-600 px-3 py-2 text-sm"
                />
            </div>
        </div>

        <div class="overflow-x-auto">
            <Table class="w-full border-collapse">
                <TableHeader>
                    <TableRow>
                        <TableHead class="w-24 p-2 text-center bg-slate-800"
                            >Čas</TableHead
                        >
                        {#each days as day}
                            <TableHead
                                class="w-1/6 p-2 text-center bg-slate-800"
                                >{day}</TableHead
                            >
                        {/each}
                    </TableRow>
                </TableHeader>
                <TableBody>
                    {#each timeSlots as timeSlot}
                        <TableRow>
                            <TableCell
                                class="font-medium p-2 text-center border border-slate-700 bg-slate-800"
                            >
                                {timeSlot}
                            </TableCell>
                            {#each days as day}
                                <TableCell class="p-1 border border-slate-700">
                                    {#if schedule[day] && schedule[day][timeSlot]}
                                        <div
                                            class="bg-slate-800 hover:bg-slate-700 transition-all duration-200 hover:text-primary hover:scale-[1.03] p-2 h-full flex flex-col justify-center rounded-md"
                                        >
                                            <div class="font-bold text-sm">
                                                {schedule[day][timeSlot]
                                                    .subject}
                                            </div>
                                            <div
                                                class="text-xs text-slate-400 mt-1"
                                            >
                                                {schedule[day][timeSlot].room}
                                            </div>
                                            <div class="text-xs text-slate-400">
                                                {schedule[day][timeSlot]
                                                    .teacher}
                                            </div>
                                        </div>
                                    {/if}
                                </TableCell>
                            {/each}
                        </TableRow>
                    {/each}
                </TableBody>
            </Table>
        </div>
    </div>
</div>
