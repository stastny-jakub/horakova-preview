<script>
    import {gsap} from "gsap/dist/gsap";
    import {ScrollTrigger} from "gsap/dist/ScrollTrigger";
    import {ScrollToPlugin} from "gsap/dist/ScrollToPlugin";
    import {onMount} from "svelte";

    gsap.registerPlugin(ScrollToPlugin);
    gsap.registerPlugin(ScrollTrigger);

    onMount(() => {
        let tl = gsap.timeline({
            scrollTrigger: {
                trigger: ".clients",
                start: "50% bottom",
                end: "90% bottom",
                markers: false,
                scrub: 1,
            }
        });
        tl.to(".clients .top", {
            x: "0%",
            ease: "power1.in"
        })
        tl.to(".clients .bottom", {
            x: "0%",
            ease: "power1.in"
        }, "<")
        gsap.fromTo(".clients .top .group", {
            translateX: 0
        }, {
            translateX: 100 + "%",
            repeat: -1,
            duration: 20,
            ease: "linear",
        })
        gsap.fromTo(".clients .bottom .group", {
            translateX: 0
        }, {
            translateX: -100 + "%",
            repeat: -1,
            duration: 30,
            ease: "linear",
        })
    });
</script>
<section class="clients" id="clients">
    <div class="text-container">
        Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad
    </div>
    <div class="slider top">
        <div class="group">
            <div class="slide">
                <img src="./miton.png" alt="">
                <img src="./miton-color.png" alt="">
            </div>
            <div class="slide">
                <img src="./miton.png" alt="">
                <img src="./miton-color.png" alt="">
            </div>
            <div class="slide">
                <img src="./miton.png" alt="">
                <img src="./miton-color.png" alt="">
            </div>
            <div class="slide">
                <img src="./miton.png" alt="">
                <img src="./miton-color.png" alt="">
            </div>
        </div>
        <div class="group">
            <div class="slide">
                <img src="./miton.png" alt="">
                <img src="./miton-color.png" alt="">
            </div>
            <div class="slide">
                <img src="./miton.png" alt="">
                <img src="./miton-color.png" alt="">
            </div>
            <div class="slide">
                <img src="./miton.png" alt="">
                <img src="./miton-color.png" alt="">
            </div>
            <div class="slide">
                <img src="./miton.png" alt="">
                <img src="./miton-color.png" alt="">
            </div>
        </div>
    </div>
    <div class="slider bottom">
        <div class="group">
            <div class="slide">
                <img src="./miton.png" alt="">
                <img src="./miton-color.png" alt="">
            </div><div class="slide">
            <img src="./miton.png" alt="">
            <img src="./miton-color.png" alt="">
        </div><div class="slide">
            <img src="./miton.png" alt="">
            <img src="./miton-color.png" alt="">
        </div><div class="slide">
            <img src="./miton.png" alt="">
            <img src="./miton-color.png" alt="">
        </div><div class="slide">
            <img src="./miton.png" alt="">
            <img src="./miton-color.png" alt="">
        </div>
        </div>
        <div class="group">
            <div class="slide">
                <img src="./miton.png" alt="">
                <img src="./miton-color.png" alt="">
            </div><div class="slide">
            <img src="./miton.png" alt="">
            <img src="./miton-color.png" alt="">
        </div><div class="slide">
            <img src="./miton.png" alt="">
            <img src="./miton-color.png" alt="">
        </div><div class="slide">
            <img src="./miton.png" alt="">
            <img src="./miton-color.png" alt="">
        </div><div class="slide">
            <img src="./miton.png" alt="">
            <img src="./miton-color.png" alt="">
        </div>
        </div>
    </div>
</section>

<style lang="scss">
    .clients {
        width: 100%;
        height: 100vh;
        display: flex;
        position: relative;
        flex-direction: column;
        justify-content: center;
        overflow: hidden;
        .text-container {
            color: white;
            text-align: center;
            width: min(500px, 100%);
            margin-inline: auto;
            padding-bottom: 40px;
        }
        .top {
            width: 100%;
            transform: translateX(-100%);

            &.slider {
                display: flex;
                overflow: hidden;
                justify-content: flex-end;

                .group {
                    display: flex;
                }

                .slide {
                    height: clamp(150px, 20vw, 280px);
                    padding: clamp(20px, 4vw, 40px);
                    border: solid 1px white;
                    width: 25vw;
                    flex-shrink: 0;
                    border-left: none;
                    cursor: pointer;
                    display: flex;
                    position: relative;
                    overflow: hidden;
                    flex-direction: column;

                    img {
                        height: 100%;
                        width: 100%;
                        object-fit: contain;
                    }
                    img:first-child {
                        transform: translateY(50%);
                    }
                    img:last-child{
                        transform: translateY(-50%);
                        opacity: 0;
                        transition: opacity 0.3s ease;
                    }
                    &:hover {
                        img:last-child {
                            opacity: 1;
                        }
                    }
                }
            }
        }

        .bottom {
            width: 100%;
            transform: translateX(100%);

            &.slider {
                display: flex;
                overflow: hidden;
                justify-content: flex-start;

                .group {
                    display: flex;
                }

                .slide {
                    height: clamp(150px, 20vw, 280px);
                    padding: clamp(20px, 4vw, 40px);
                    border: solid 1px white;
                    width: 20vw;
                    flex-shrink: 0;
                    border-left: none;
                    cursor: pointer;
                    display: flex;
                    position: relative;
                    overflow: hidden;
                    flex-direction: column;

                    img {
                        height: 100%;
                        width: 100%;
                        object-fit: contain;
                    }
                    img:first-child {
                        transform: translateY(50%);
                    }
                    img:last-child{
                        transform: translateY(-50%);
                        opacity: 0;
                        transition: opacity 0.3s ease;
                    }
                    &:hover {
                        img:last-child {
                            opacity: 1;
                        }
                    }
                }
            }
        }
    }
    @media only screen and (max-width: 800px) {
        .clients {
            .top {
                .slide {
                    width: 50vw !important;
                }
            }
            .bottom {
                .slide {
                    width: 33.333vw !important;
                }
            }
        }
    }
</style>
