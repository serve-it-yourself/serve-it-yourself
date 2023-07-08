<script lang="ts">
    import '@skeletonlabs/skeleton/themes/theme-modern.css';
    import '@skeletonlabs/skeleton/styles/skeleton.css';
    import "../app.postcss";

    import {AppShell, AppRail, AppRailTile, AppRailAnchor, AppBar} from '@skeletonlabs/skeleton';
    import {TitleStore} from "../stores/title_store";

    let titleList = [
        {title: "Jetti", route: "/jetti"},
        {title: "lux", route: "/lux"},
        {title: "sona", route: "/sona"},
        {title: "thresh", route: "/thresh"},
    ];

    let currentTile: number = 0;
    let currentTitle: string = $TitleStore;

    TitleStore.subscribe((value) => {
        currentTitle = value;
    });
</script>

<AppShell>
    <svelte:fragment slot="header">
        <AppBar gridColumns="grid-cols-3" slotDefault="place-self-center" slotTrail="place-content-end">
            <svelte:fragment slot="lead"></svelte:fragment>
            {currentTitle}
            <svelte:fragment slot="trail"></svelte:fragment>
        </AppBar>
    </svelte:fragment>
    <svelte:fragment slot="sidebarLeft">
        <AppRail>
            <svelte:fragment slot="lead">
                <AppRailAnchor href="/">Index</AppRailAnchor>
            </svelte:fragment>
            {#each titleList as title}
                <AppRailTile bind:group={currentTile} name={title.title} value={title.route} title={title.title}>
                    <svelte:fragment slot="lead"></svelte:fragment>
                    <span>{title.title}</span>
                </AppRailTile>
            {/each}
        </AppRail>
    </svelte:fragment>
    <!-- (sidebarRight) -->
    <!-- (pageHeader) -->
    <!-- Router Slot -->
    <slot/>
    <!-- ---- / ---- -->
    <!-- (pageFooter) -->
    <svelte:fragment slot="footer">This site is a introduction of "Serve it Yourself!!" project.</svelte:fragment>
</AppShell>
