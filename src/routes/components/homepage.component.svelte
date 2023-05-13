<script>
    import {gsap} from "gsap/dist/gsap";
    import {onMount} from "svelte";
    import Navigation from "./homepage.components/navigation.component.svelte"

    let moveAnimation;
    let canMove = true;

    let section;
    let notebook;
    let nav;
    let frontCloud;
    let cloudContainer;

    let timeout;

    const handleMouseMove = (e) => {
        if (canMove) {
            let el = document.querySelector(".homepage");
            let rect = el.getBoundingClientRect();
            let onePercentX = rect.width / 100;
            let onePercentY = rect.height / 100;
            let index = 0.1;
            moveAnimation?.kill();
            moveAnimation = gsap.to(".cloud-container > *", {
                x: (e.clientX / onePercentX - 50) * index + "%",
                y: (e.clientY / onePercentY - 50) * index + "%",
                duration: 2
            })
        }
    }

    const addAnimations = (tl) => {
        tl.clear();
        tl.to(notebook, {
            x: "-50%",
            y: "-50%",
            top: "50%",
            left: "50%",
            duration: 0.2,
            rotate: 0
        })
        tl.to(frontCloud, {
            opacity: 0,
            duration: 0.05
        }, "<")
        tl.to(notebook, {
            width: "100vw",
            height: "100vh",
        }, "<")
        tl.fromTo(nav, {
                rotate: 0,
                scale: 1
            },
            {
                rotate: 90,
                scale: 3
            }, "<")
        tl.fromTo(".cloud-container > *:not(.notebook)", {
            rotate: 0,
            scale: 1
        }, {
            rotate: 90,
            scale: 0,
        }, "<")
    }
    onMount(() => {
        let tl = gsap.timeline({
            scrollTrigger: {
                trigger: section,
                scrub: 1,
                start: "top+=1 top",
                end: "100% top",
                pin: true,
                markers: false,
                pinSpacing: false,
                onEnter: self => {
                    clearTimeout(timeout);
                    canMove = false;
                    moveAnimation?.kill();
                    addAnimations(tl);
                },
                onLeaveBack: self => {
                    timeout = setTimeout(() => {
                        canMove = true;
                    }, 1000)
                },
                onLeave: self => {
                    gsap.set(cloudContainer, {
                        display: "none"
                    }, ">")
                },
                onEnterBack: self => {
                    gsap.set(cloudContainer, {
                        display: "flex"
                    }, ">")
                }
            }
        });
    })
</script>
<section class="homepage" bind:this={section} id="home">
    <Navigation bind:navBind={nav}/>
    <div class="canvas" on:mousemove={handleMouseMove}>
        <div bind:this={cloudContainer} class="cloud-container">
            <img class="cloud" src="/cloud.png" alt=""/>
            <div bind:this={notebook} class="notebook">
                <img src="/ntb_bottom.png" alt="">
            </div>
            <img bind:this={frontCloud} src="/cloud_front.png" alt="" class="cloud-front"/>
            <span>Je to hra se slovy..<br>to děláme<br>"venture" capital</span>
            <h1>The Law of<br>Adventure</h1>
        </div>
    </div>
</section>
<style lang="scss">
    @import "../../style";

    section {
        width: 100%;
        max-width: 100%;
        height: 100vh;
        display: grid;
        grid-template-columns: $navWidth auto $navWidth;
        grid-template-rows: $navWidth auto $navWidth;
        overflow: hidden;

        .canvas {
            grid-column: 2 / 3;
            grid-row: 2 / 3;
            position: relative;
            display: flex;
            justify-content: center;
            align-items: center;


            .cloud-container {
                font-size: 1.8vw;
                position: relative;

                h1 {
                    font-size: 3em;
                    color: white;
                    font-family: "Abril Fatface", sans-serif;
                    position: absolute;
                    left: 0;
                    top: 0;
                    margin: 0;
                    line-height: 1.1;
                    transform-origin: right bottom;
                }

                span {
                    font-size: 1em;
                    color: white;
                    font-family: "Open Sans", sans-serif;
                    position: absolute;
                    right: 0;
                    bottom: 0;
                    margin: 0;
                    font-weight: 100;
                    line-height: 1.1;
                    transform-origin: left top;
                }

                .cloud-front {
                    position: absolute;
                    left: 0;
                    top: 0;
                    width: 35em;
                    z-index: 10;
                }

                .notebook {
                    position: absolute;
                    left: 18.5em;
                    top: 3.5em;
                    background-color: white;
                    height: 7.5em;
                    width: 10em;
                    background-image: url("/original_cloud.png");
                    background-size: cover;
                    z-index: 10;
                    transform: rotate(-20deg);
                    border-radius: 1px;
                    box-shadow: black 0 0 0 6px, #333333 0 0 0 7px, #434343 0 0 0 8px, #626262 0 0 0 9px;
                    img {
                        position: absolute;
                        top: calc(100% + 9px);
                        left: 50%;
                        transform: translateX(-50%);
                        width: 120%;
                    }
                }

                .cloud, .cloud-front {
                    width: 35em;
                }
            }
        }
        @media only screen and (max-width: 800px) {
            .canvas {
                grid-column: 1 / 4;
                .cloud-container {
                    font-size: 2.3vw;
                    width: 100%;
                    h1 {
                        font-size: 5em;
                        width: 100%;
                        text-align: center;
                        bottom: 60%;
                        top: unset;
                    }
                    .cloud {
                        width: 40em;
                    }
                    span {
                        width: 100%;
                        text-align: center;
                        font-size: 1.5em;
                        bottom: unset;
                        top: 80%;
                    }
                    .notebook {
                        height: 7.5em;
                        width: 5em;
                        left: 21.5em;
                        top: 4.5em;
                        img {
                            display: none;
                        }
                    }
                }
            }
        }
        @media only screen and (max-width: 500px) {
            .canvas {
                max-width: 100vw;
                .cloud-container {
                    h1 {
                        font-size: 6em;
                    }
                    .cloud, .cloud-front {
                        width: 100%;
                    }
                }
            }
        }
    }
</style>
