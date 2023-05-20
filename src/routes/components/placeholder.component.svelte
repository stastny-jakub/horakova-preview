<section id="members" class="members">
    <div class="left-line">
        <div class="line"></div>
    </div>
    <div class="right-line">
        <div class="line"></div>
    </div>
    <div class="bottom-line">
        <div class="l-corner"></div>
        <div class="hor-line"></div>
        <div class="r-corner"></div>
    </div>
    <div class="canvas">
        <span>Oddíl s členy</span>
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

        .canvas {
            grid-area: 2 / 2 / 3 / 3;
            display: flex;
            justify-content: center;
            align-items: center;
            & > span {
                font-size: 30px;
                color: white;
                font-weight: bold;
            }
        }

        .left-line, .right-line {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-end;

            .line {
                width: 1px;
                height: 100%;
                background-color: $borderColor;
            }
        }

        .left-line {
            grid-area: 1 / 1 / 3 / 2;
        }
        .right-line {
            grid-area: 1 / 3 / 3 / 4;
        }
        .bottom-line {
            grid-area: 3 / 1 / 4 / 4;
            display: flex;
            align-items: center;
            .hor-line {
                height: 1px;
                width: 100%;
                background-color: $borderColor;
            }
            .l-corner {
                width: 1px;
                height: calc(50% + 1px);
                background-color: $borderColor;
                margin-bottom: auto;
                margin-left: calc($navWidth / 2 - 0.5px);
            }
            .r-corner {
                width: 1px;
                height: calc(50% + 1px);
                background-color: $borderColor;
                margin-bottom: auto;
                margin-right: calc($navWidth / 2 - 0.5px);
            }
        }
    }
    @media only screen and (max-width: 800px) {
        .members {
            .left-line, .right-line, .r-corner, .l-corner {
                display: none;
            }
        }
    }
</style>
