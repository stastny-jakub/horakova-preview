<script>
    import {gsap} from "gsap/dist/gsap";
    import {ScrollTrigger} from "gsap/dist/ScrollTrigger";
    import {ScrollToPlugin} from "gsap/dist/ScrollToPlugin";
    import {onMount} from "svelte";
    import GlobalNavigation from "./global.components/navigation.component.svelte"

    gsap.registerPlugin(ScrollToPlugin);
    gsap.registerPlugin(ScrollTrigger);

    let left;
    let wrapper;

    let animation;
    let nav;

    let expertiseItems = [
        {
            text: "Venture capital",
            imgPath: "./unicorn.svg"
        },
        {
            text: "Intelectual property",
            imgPath: "./mind.svg"
        },
        {
            text: "Coporate law",
            imgPath: "./house.svg"
        },
        {
            text: "Crypto assets",
            imgPath: "./documents.svg"
        },
        {
            text: "M&A",
            imgPath: "./crypto.svg"
        },
        {
            text: "open banking",
            imgPath: "./conversion.svg"
        },
    ]

    const handleMove = (e) => {
        let leftContainer = left.getBoundingClientRect()
        let wrapperContainer = wrapper.getBoundingClientRect();

        let absolutePositionY = e.clientY - leftContainer.top
        let onePercentY = leftContainer.height / 100;
        let relativePositionYRaw = (absolutePositionY / onePercentY);
        let relativePositionY = (absolutePositionY / onePercentY - 50) * 2;

        let absolutePositionX = e.clientX - leftContainer.left
        let onePercentX = leftContainer.width / 100;
        let relativePositionX = (absolutePositionX / onePercentX);

        let overflow = (wrapperContainer.height - leftContainer.height) / 2 + 40;
        animation = gsap.to(wrapper, {
            duration: 0.5,
            y: overflow * (-relativePositionY / 100)
        })
        let xTransformIndex = 5

    }
    const handleOver = (e) => {
        let target = e.currentTarget.dataset.for;
        let targetText = e.currentTarget.dataset.fortext;
        let targetEl = document.querySelector(`#${target}`);
        let targetElText = document.querySelector(`#${targetText}`);
        let otherEl = document.querySelectorAll(`.expertise .right > div:not(#${target})`);
        let otherElText = document.querySelectorAll(`.expertise .right > p:not(#${target})`);

        gsap.killTweensOf(targetEl);
        gsap.killTweensOf(otherEl);

        gsap.set(targetEl, {
            zIndex: 1
        })
        gsap.set(otherEl, {
            zIndex: 0
        })
        gsap.to(otherEl, {
            scale: 0,
            duration: 0.1
        })
        gsap.to(targetEl, {
            scale: 1,
            ease: "back.out"
        })
        gsap.to(otherElText, {
            opacity: 0,
            duration: 0.1
        })
        gsap.to(targetElText, {
            opacity: 1,
            ease: "back.out"
        })
    }

    onMount(() => {
        let tl = gsap.timeline({
            scrollTrigger: {
                trigger: ".expertise",
                start: "top bottom",
                end: "bottom bottom",
                scrub: 1,
                markers: false,
            },

        });
        tl.to([".expertise .left-line .line", ".expertise .right-line .line"], {
            height: "100%",
        })
        tl.to([".expertise .left", ".expertise .right"], {
            x: "0%",
        }, "<")
        tl.from(nav, {
            yPercent: -100,
        }, "<")
    });
</script>
<GlobalNavigation bind:navBind={nav}></GlobalNavigation>
<section class="expertise" id="expertise">
    <div class="left-line">
        <div class="line"></div>
    </div>
    <div class="right-line">
        <div class="line"></div>
    </div>
    <div class="canvas">
        <div class="left" bind:this={left} on:mousemove={handleMove}>
            <div class="wrapper" bind:this={wrapper}>
                {#each expertiseItems as item, index}
                    <span data-for={"expertise-item-" + index} data-fortext={"expertise-text-" + index} on:mouseover={handleOver}>{item.text}</span>
                {/each}
            </div>
        </div>
        <div class="right">
            {#each expertiseItems as item, index}
                <div id={"expertise-item-" + index} style:background-image={"url('" + item.imgPath + "')"}
                     class="image"></div>
                <p id={"expertise-text-" + index} class="text">Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad</p>
            {/each}
        </div>
    </div>
</section>
<style lang="scss">
    @import "../../style";

    .expertise {
        width: 100%;
        height: 100vh;
        display: grid;
        grid-template-columns: $navWidth auto $navWidth;
        grid-template-rows: $navWidth auto $navWidth;
        overflow: hidden;

        .canvas {
            grid-area: 2 / 2 /3 /3;
            display: flex;
            align-items: center;

            .left {
                transform: translateX(calc(-100% - $navWidth));
                height: 400px;
                overflow: hidden;
                position: relative;
                display: flex;
                align-items: center;
                mask-image: linear-gradient(transparent, white 15%, white 85%, transparent);
                width: 60%;
                .wrapper {
                    display: flex;
                    flex-direction: column;

                    span {
                        font-size: clamp(30px, 5vw, 50px);
                        color: transparent;
                        background-image: linear-gradient(to right, white 50%, transparent 50%);
                        background-position: 100%;
                        background-size: 200% 100%;
                        -webkit-text-stroke: 1px white;
                        text-transform: uppercase;
                        font-weight: 900;
                        line-height: 2;
                        transition: all 0.5s;
                        position: relative;
                        background-clip: text;
                        -webkit-background-clip: text;

                        &:hover {
                            background-position: 0;
                        }
                    }
                }
            }

            .right {
                width: 40%;
                flex-grow: 1;
                height: 100%;
                transform: translateX(calc(100% + $navWidth));
                margin-left: 20px;
                display: flex;
                position: relative;
                justify-content: center;
                align-items: flex-end;
                .text {
                    color: white;
                    opacity: 0;
                    position: absolute;
                    left: 0;
                    bottom: 0;
                    right: 0;
                    text-align: center;
                }
                .image {
                    position: absolute;
                    left: 50%;
                    top: 50%;
                    transform: translate(-50%, -50%) scale(0);
                    height: 50%;
                    width: 50%;
                    background-position: center;
                    background-size: contain;
                    background-repeat: no-repeat;
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
        .expertise {
            .canvas {
                grid-area: 2 / 1 /3 /4;
                .right {
                    display: none;
                }
                .left {
                    width: 100%;
                    padding-inline: 20px;
                    transform: translateX(-100%);
                    justify-content: center;
                }
            }
            .left-line, .right-line {
                display: none;
            }
        }
    }
</style>
