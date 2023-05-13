<script>
    import {gsap} from "gsap/dist/gsap";
    import {onMount} from "svelte";
    let progress;
    let loader;
    let self;
    onMount(()=>{
        let tl = gsap.timeline({});
        tl.to(loader, {
            height: 100 + "%",
            duration: 4,
            ease: "expo",
            onUpdate: args => {
                progress = parseInt(loader?.style.height)
            }
        })
        tl.to(self, {
            opacity: 0,
            onComplete: args => {
                document.body.classList.remove("loading")
                self.style.display = "none"
            }
        }, ">")
    })
</script>
<div bind:this={self} class="loading-container">
    <div class="counter">{progress}%</div>
    <div bind:this={loader} class="loader"></div>
</div>
<style lang="scss">
    .loading-container {
        height: 100vh;
        width: 100%;
        display: flex;
        align-items: flex-end;
        background-color: white;
        position: fixed;
        left: 0;
        top: 0;
        z-index: 1000;
        .loader {
            width: 100%;
            height: 0;
            background-color: #D38393;
        }
        .counter {
            position: absolute;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%);
            color: white;
            font-size: 40px;
        }
    }
</style>
