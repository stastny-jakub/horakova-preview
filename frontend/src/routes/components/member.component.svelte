<script>
    import {gsap} from "gsap/dist/gsap";
    import {ScrollTrigger} from "gsap/dist/ScrollTrigger";
    import {ScrollToPlugin} from "gsap/dist/ScrollToPlugin";
    import {onMount} from "svelte";

    gsap.registerPlugin(ScrollToPlugin);
    gsap.registerPlugin(ScrollTrigger);

    let container;
    let photo;
    let textWrapper;

    onMount(() => {
        return
        let tl1 = gsap.timeline({
            scrollTrigger: {
                trigger: container,
                start: "25% bottom",
                end: "75% bottom",
                scrub: 1,
            }
        });
        tl1.to([photo, textWrapper], {
            y: "50%",
            bottom: "45%"
        })

        let tl2 = gsap.timeline({
            scrollTrigger: {
                trigger: container,
                start: "bottom bottom",
                end: "bottom+=100% bottom",
                pin: true,
                scrub: 1,
            }
        });
        tl2.to(photo, {
            x: "-50%",
        })
        tl2.to(textWrapper, {
            x: "50%",
            width: "600px"
        }, "<")
    });
</script>
<section class="members" bind:this={container}>
    <div class="left-line">
        <div class="line"></div>
    </div>
    <div class="right-line">
        <div class="line"></div>
    </div>
    <div class="wrapper">
        <div class="photo" bind:this={photo}></div>
        <div class="text-wrapper" bind:this={textWrapper}>
            <h2>Bohuslava Horakova</h2>
            <p>
                Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut
                laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad
            </p>
        </div>
    </div>
</section>
<style lang="scss">
    @import "../../style";


    .members {
        width: 100%;
        height: 100vh;
        display: grid;
        grid-template-columns: $navWidth auto $navWidth;
        grid-template-rows: $navWidth auto $navWidth;
        overflow: hidden;
        position: relative;
        outline: solid 1px green;

        .wrapper {
            display: flex;
            align-items: center;
            justify-content: center;
            outline: solid red 1px;
            margin: auto;
            max-width: 100%;
            grid-area: 2 / 2 /3 /3;

            .photo {
                width: 500px;
                aspect-ratio: 22 / 31;
                background-image: url("./woman.jpg");
                background-size: cover;
                background-position: center;
                position: relative;

                &::after {
                    position: absolute;
                    inset: 0;
                    content: "";
                    background-image: url("./photo-frame.svg");
                    background-position: right top;
                    background-repeat: no-repeat;
                    background-size: contain;
                    transform: translate(20px, -20px);
                }
            }

            .text-wrapper {
                padding-left: 50px;
                outline: solid blue 1px;
                max-width: 50%;
                h2 {
                    font-size: 58px;
                    font-weight: bold;
                    color: white;
                    white-space: nowrap

                }
            }
        }

        .left-line, .right-line {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-end;

            .line {
                width: 1px;
                height: 100px;
                background-color: $borderColor;
            }
        }

        .left-line {
            grid-area: 1 / 1 / 4 / 2;
        }

        .right-line {
            grid-area: 1 / 3 / 4 / 4;
        }
    }
    @media only screen and (max-width: 800px) {
    }
</style>
