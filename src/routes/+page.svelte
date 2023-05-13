<script>
    import Homepage from "./components/homepage.component.svelte";
    import Expertise from "./components/expertise.component.svelte"
    import Loading from "./components/loading.component.svelte"
    import Member from "./components/member.component.svelte";
    import Clients from "./components/clients.component.svelte"
    import GlobalNavigation from "./components/global.components/navigation.component.svelte"
</script>



    <Homepage></Homepage>
    <div class="spacing"></div>
    <Expertise></Expertise>
    <Clients></Clients>


<style lang="scss">
    .spacing {
        width: 100%;
        height: 70vh;
    }
</style>
