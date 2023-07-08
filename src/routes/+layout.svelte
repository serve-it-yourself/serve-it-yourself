<script lang="ts">
    import {
        Header,
        HeaderNav,
        HeaderNavItem,
        SideNav,
        SideNavItems,
        SideNavLink,
        SkipToContent,
        Content,
        Grid,
        Row,
        Column,
    } from "carbon-components-svelte";
    import Fade from "carbon-icons-svelte/lib/Fade.svelte";

    import "carbon-components-svelte/css/white.css";
    import {page} from "$app/stores";

    let isSideNavOpen = false;

    let items = [
        {text: "Index", href: "/", isSelected: false},
        {text: "Jetti", href: "/jetti", isSelected: false},
        {text: "Lux", href: "/lux", isSelected: false},
        {text: "Sona", href: "/sona", isSelected: false},
        {text: "Thresh", href: "/thresh", isSelected: false},
        {text: "Mediator", href: "/mediator", isSelected: false},
    ];

    $: items = items.map((item) => {
        item.isSelected = item.href === $page.url.pathname;
        return item;
    });
</script>

<Header company="IBM" platformName="Carbon Svelte" bind:isSideNavOpen>
    <svelte:fragment slot="skip-to-content">
        <SkipToContent />
    </svelte:fragment>
    <HeaderNav>
        {#each items as item}
            <HeaderNavItem href={item.href} text={item.text} />
        {/each}
    </HeaderNav>
</Header>

<SideNav bind:isOpen={isSideNavOpen} rail>
    <SideNavItems>
        {#each items as item}
            <SideNavLink icon={Fade} text={item.text} href={item.href} isSelected={item.isSelected} />
        {/each}
    </SideNavItems>
</SideNav>

<Content>
    <Grid>
        <Row>
            <Column>
                <slot />
            </Column>
        </Row>
    </Grid>
</Content>