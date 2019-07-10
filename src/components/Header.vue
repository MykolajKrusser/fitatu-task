<template>
    <header class="page-header">
        <div class="page-header__content">
            <div class="page-header__logo" @click="onLogoClick">
                <Logo />
            </div>
            <nav class="page-header__nav" v-bind:class="[mobNavStatus ? navigationOpen : navigationClose]">
                <a href="#">Home</a>
                <a href="#">Our Fitatu</a>
                <a href="#">Team</a>
                <a href="#">Contact</a>
                <a href="#">Products</a>
            </nav>
            <div id="menuToggle">
                <input type="checkbox" v-on:click="mobNavHandler"/>
                <span id="span1"></span>
                <span id="span2"></span>
                <span id="span3"></span>
            </div>
        </div>
    </header>
</template>
<script>
    import Logo from '@img/fitatu.svg';

    export default {
        props: {
            onLogoClick: {
                type: Function,
                default: () => {},
            },
        },
        data() {
            return {
                navigationOpen: 'navigationOpen',
                navigationClose: 'navigationClose',
                mobNavStatus: false
            }
        },
        methods: {
            mobNavHandler(e){
                this.mobNavStatus = e.target.checked;
            }
        },
        components: {
            Logo,
        },
    };
</script>
<style lang="scss" scoped>
    .page-header {
        height: 60px;
        width: 100vw;

        &__content {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 25px;
            position: fixed;
            z-index: 11;
            height: inherit;
            width: 100%;
            background-color: #fff;
            box-shadow: 0 0 15px #ced0d0;
        }

        &__logo {
            cursor: pointer;
        }

        &__nav {
            display: flex;
            flex-direction: row;
            justify-content: space-between;
            
            a {
                color: black;
                text-decoration: none;
                margin: 10px;
                border: 1px solid transparent;
                padding: 2px;
                transition: all 0.3s ease;
                &:hover {
                    border-bottom: 1px solid #ec4217;
                    transition: all 0.3s ease;
                }
            }
        }
        /*
            hamburger menu button
        */
        #menuToggle {
            overflow: hidden;
            position: relative;
            height: 100%;
            display: none;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            margin-top: 8px;
        }

        #menuToggle input {
            display: flex;
            width: 60px;
            height: 60px;
            position: absolute;
            cursor: pointer;
            opacity: 0; /* hide input */
            z-index: 1; /* top of the menu */
        }

        #menuToggle span{
            width: 55px;
            height: 8px;
            margin-bottom: 10px;
            background: #7f8fa6;
            border-radius: 4px;
            transition: all .5s cubic-bezier(.08,.81,.87,.71);
        }

        #span1 {
            transform-origin: 4px 0px;
        }

        #span3 {
            transform-origin: bottom right;
        }

        #menuToggle input:checked ~ #span1 {
            background-color: #0c2461;
            transform: rotate(45deg) translate(8px);
        }
        #menuToggle input:checked ~ #span2 {
            background-color: #0c2461;
            transform: rotate(495deg) translate(4px);   
        }
        #menuToggle input:checked ~ #span3 {
            background-color: #0c2461;
            transform: rotate(45deg);
            opacity: 0;
        }

        @media screen and (max-width: 1024px){
            #menuToggle{
                display: flex;
            }
            .page-header__nav{
                position: fixed;
                top: 0;
                left: 0;
                min-width: 70%;
                height: 100vh;
                display: flex;
                flex-wrap: wrap;
                flex-direction: column;
                justify-content: center;
                align-items: center;
                box-sizing: border-box;
                transition: all 1s ease-out;
                background: rgba(148, 148, 148, 0.932);
                box-shadow: inset 0px 0px 40px 7px rgba(255, 255, 255, 0.41);
                z-index: 888;
                
                a {
                    color: white;
                    font-size: 22px;
                }
            }

            .navigationOpen{
                opacity: 1;
                transform: translateX(0);
            }

            .navigationClose{
                opacity: 0;
                transform: translateX(200%);
            }
        }
    }
</style>