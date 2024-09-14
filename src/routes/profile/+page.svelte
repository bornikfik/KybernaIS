<script lang="ts">
    import { Button } from '$lib/components/ui/button';
    import {
        Card,
        CardContent,
        CardHeader,
        CardTitle,
    } from '$lib/components/ui/card';
    import { Input } from '$lib/components/ui/input';
    import { Label } from '$lib/components/ui/label';
    import {
        Tabs,
        TabsList,
        TabsTrigger,
        TabsContent,
    } from '$lib/components/ui/tabs/index';
    import {
        Avatar,
        AvatarImage,
        AvatarFallback,
    } from '$lib/components/ui/avatar';
    import { Wifi, QrCode } from 'lucide-svelte';

    let username = 'Načti @ssaklk.cz';
    let password = '';
</script>

<div class="container mx-auto p-4">
    <h1 class="text-2xl font-bold mb-6">Profil uživatele</h1>
    <div class="grid gap-6 md:grid-cols-2">
        <Card>
            <CardHeader class="flex flex-row items-center gap-4">
                <Avatar class="w-20 h-20">
                    <AvatarImage
                        src="/placeholder.svg?height=80&width=80"
                        alt="Profile picture"
                    />
                    <AvatarFallback>VS</AvatarFallback>
                </Avatar>
                <div>
                    <CardTitle>Viktor Škarda</CardTitle>
                    <p class="text-sm text-muted-foreground">
                        skarda.viktor@ssaklk.cz
                    </p>
                </div>
            </CardHeader>
            <CardContent>
                <div class="grid gap-2">
                    <div class="grid grid-cols-2 gap-1">
                        <Label for="jmeno">Jméno</Label>
                        <Input
                            id="jmeno"
                            value="Viktor"
                            readonly
                        />
                    </div>
                    <div class="grid grid-cols-2 gap-1">
                        <Label for="prijmeni">Příjmení</Label>
                        <Input
                            id="prijmeni"
                            value="Škarda"
                            readonly
                        />
                    </div>
                    <div class="grid grid-cols-2 gap-1">
                        <Label for="email">Školní e-mail</Label>
                        <Input
                            id="email"
                            value="skarda.viktor@ssaklk.cz"
                            readonly
                        />
                    </div>
                </div>
            </CardContent>
        </Card>

        <Card>
            <CardHeader>
                <CardTitle>Seznam skupin</CardTitle>
            </CardHeader>
            <CardContent>
                <Tabs value="rozdeleni">
                    <TabsList class="grid w-full grid-cols-3">
                        <TabsTrigger value="rozdeleni"
                            >Rozdělení třídy</TabsTrigger
                        >
                        <TabsTrigger value="bloky">Bloky</TabsTrigger>
                        <TabsTrigger value="projekty">Projekty</TabsTrigger>
                    </TabsList>
                    <TabsContent
                        value="rozdeleni"
                        class="mt-4"
                    >
                        <div class="grid gap-2">
                            <div class="flex justify-between">
                                <span>1</span>
                                <span>p</span>
                            </div>
                        </div>
                    </TabsContent>
                    <TabsContent
                        value="bloky"
                        class="mt-4"
                    >
                        <div class="grid gap-2">
                            <div class="flex justify-between">
                                <span>Předmět</span>
                                <span>Název</span>
                            </div>
                        </div>
                    </TabsContent>
                    <TabsContent
                        value="projekty"
                        class="mt-4"
                    >
                        <p>Žádné projekty k zobrazení.</p>
                    </TabsContent>
                </Tabs>
                <p class="text-xs text-muted-foreground mt-4">
                    Žluté označení skupiny není povinná (nepovinný volitelný
                    předmět)
                </p>
            </CardContent>
        </Card>

        <Card>
            <CardHeader>
                <CardTitle class="flex items-center gap-2">
                    <Wifi class="w-5 h-5" />
                    Nastavení Wifi
                </CardTitle>
            </CardHeader>
            <CardContent>
                <div class="grid gap-4">
                    <div class="grid grid-cols-2 gap-1">
                        <Label for="username">Uživatelské jméno</Label>
                        <Input
                            id="username"
                            bind:value={username}
                            readonly
                        />
                    </div>
                    <div class="grid grid-cols-2 gap-1">
                        <Label for="password">Heslo na eduroam</Label>
                        <div class="flex gap-2">
                            <Input
                                id="password"
                                type="password"
                                bind:value={password}
                            />
                            <Button>Uložit</Button>
                        </div>
                    </div>
                </div>
            </CardContent>
        </Card>

        <Card>
            <CardHeader>
                <CardTitle class="flex items-center gap-2">
                    <QrCode class="w-5 h-5" />
                    QR kód s vaším profilem
                </CardTitle>
            </CardHeader>
            <CardContent class="flex justify-center">
                <img
                    src="/placeholder.svg?height=200&width=200"
                    alt="QR Code"
                    class="w-48 h-48"
                />
            </CardContent>
        </Card>
    </div>
</div>
