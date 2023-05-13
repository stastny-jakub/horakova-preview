<script>
    export let navBind;
</script>

<nav bind:this={navBind}>
    <div class="top">
        <a class="mobile-menu" href="">
            <svg width="37" height="37" viewBox="0 0 37 37" fill="none" xmlns="http://www.w3.org/2000/svg">
                <g clip-path="url(#clip0_155_1430)">
                    <path fill-rule="evenodd" clip-rule="evenodd"
                          d="M0.00585938 0H5.73743V15.7931C7.27626 13.9277 9.99994 11.5803 12.7716 12.1053C16.9401 12.8947 19.0242 15.2632 19.0242 22.8948C19.0242 23.2498 19.0236 23.597 19.0231 23.936C19.0118 30.88 19.0062 34.3635 23.9742 32.1054C26.949 30.7532 29.5699 26.9975 31.269 23.8416V2.83811e-06H37.0006V36.8421H31.269V28.5931C28.2903 32.2169 23.6471 36.8421 20.8479 36.8421C17.008 36.8421 13.5532 36.8421 13.5532 24.2105C13.5532 12.5167 9.08764 16.6103 5.73743 19.7881V36.8421H0.00585938V0Z"
                          fill="white"/>
                </g>
                <defs>
                    <clipPath id="clip0_155_1430">
                        <rect width="37" height="37" fill="white"/>
                    </clipPath>
                </defs>
            </svg>
        </a>
        <a href="" class="active">About</a>
        <div class="horizontal-line"></div>
        <a href="">Expertise</a>
        <div class="horizontal-line"></div>
        <a href="">Members</a>
        <div class="horizontal-line"></div>
        <a href="">Clients</a>
        <a class="mobile-menu" href=""><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M3 7H21" stroke="white" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M3 12H21" stroke="white" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M3 17H21" stroke="white" stroke-width="1.5" stroke-linecap="round"/>
        </svg>
        </a>
    </div>
</nav>
<style lang="scss">
    @import "../../../style";

    $borderColor: white;
    nav {
        position: fixed;
        display: flex;
        height: $navWidth;
        width: calc(100% - 2 * $navWidth);
        top: 0;
        left: 50%;
        transform: translateX(-50%);
        margin-inline: auto;
        z-index: 100;

        .top {
            display: flex;
            align-items: center;
            width: 100%;
            a {
                padding: 10px 20px;
                color: $borderColor;
                text-decoration: none;
                &.active {
                    border: solid 1px $borderColor;
                }
                &.mobile-menu {
                    display: none;
                }
            }
        }
        .horizontal-line {
            height: 1px;
            flex-grow: 1;
            background-color: $borderColor;
        }
    }
    @media only screen and (max-width: 800px){
        nav {
            width: calc(100% - 40px);
        }
    }
    @media only screen and (max-width: 600px) {
        nav {
            .top{
                a:not(.mobile-menu){
                    display: none;
                }
                a.mobile-menu {
                    display: flex;
                }
            }
        }
    }
</style>
