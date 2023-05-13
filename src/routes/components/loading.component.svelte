<script>
    import {gsap} from "gsap/dist/gsap";
    import {onMount} from "svelte";
    let progress = 0;
    let loader;
    let self;
    let counter;
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
        tl.to(counter, {
            duration: 4,
            ease: "expo",
            backgroundImage: "linear-gradient(#D38393 0%, #fff 0%)"
        }, "<")
        tl.to(self, {
            opacity: 0,
            onComplete: args => {
                document.body.classList.remove("loading")
                self.style.display = "none"
            }
        }, ">")
        document.addEventListener("scroll", ()=>{
            if(progress === 100) return;
            gsap.set(window, {
                duration: 0,
                scrollTo: { y: 0
                }
            })
        })
    })
</script>
<div bind:this={self} class="loading-container">
    <div bind:this={counter} class="counter">{progress}%</div>
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
            color: transparent;
            font-size: 70px;
            font-weight: bold;
            background-image: linear-gradient(#D38393 100%, #fff 100%);
            background-clip: text;
            -webkit-background-clip: text;
            height: 100%;
            display: flex;
            align-items: center;
        }
    }
</style>
