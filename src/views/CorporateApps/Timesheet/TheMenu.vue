<template>
    <nav>
        <img class="mb-2 mt-auto" @click="$router.push('/admin/corporate-apps')" style="cursor: pointer;" height="58" :src="rsLogo" alt="rs-logo">
        <div class="accordion-container ms-4">
            <div class="ac">
                <h2 class="ac-header">
                    <button type="button" class="ac-trigger">Manage</button>
                </h2>
                <div class="ac-panel">
                    <div class="accordion-container-child">
                        <div class="ac ps-2">
                            <h2 class="ac-header">
                                <button type="button" class="ac-trigger mx-1">Productivity Settings</button>
                            </h2>
                            <div class="ac-panel ms-1">
                                <ul class="nav nav-sm flex-column">
                                    <li class="nav-item">
                                        <router-link class="nav-link sub-menu nav-menu-font" to="screen-captures?init=0">Screen Capture Interval</router-link>
                                    </li>
                                    <li class="nav-item">
                                        <router-link class="nav-link sub-menu nav-menu-font" to="activity-notes?init=0">Activity Notes Interval</router-link>
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>
                <!-- <div class="ac-panel">
                    <ul class="nav nav-sm flex-column">
                    
                    </ul>
                </div> -->
            </div>
            <div class="ac">
                <h2 class="ac-header">
                    <button type="button" class="ac-trigger">Transact</button>
                </h2>
                <div class="ac-panel">
                    <ul class="nav nav-sm flex-column">
                        <li class="nav-item">
                            <router-link class="nav-link sub-menu nav-menu-font" to="timesheet-adjustment">Timesheet Adjustment</router-link>
                        </li>
                    </ul>
                </div>
            </div>
            <div class="ac">
                <h2 class="ac-header">
                    <button type="button" class="ac-trigger">Report</button>
                </h2>
                <div class="ac-panel">
                    <ul class="nav nav-sm flex-column">
                        <li class="nav-item">
                            <router-link class="nav-link sub-menu nav-menu-font" to="timesheet-adjustment">Screen Capture</router-link>
                        </li>
                        <li class="nav-item">
                            <router-link class="nav-link sub-menu nav-menu-font" to="timesheet-adjustment">Activity Notes</router-link>
                        </li>
                    </ul>
                </div>
            </div>
            <div class="ac">
                <h2 class="ac-header">
                    <button type="button" class="ac-trigger">Utility</button>
                </h2>
                <div class="ac-panel">
                    <ul class="nav nav-sm flex-column">

                    </ul>
                </div>
            </div>
        </div>
    </nav>
</template>
<script setup>
    import rsLogo from "@/assets/img/rs-logo-white.png";
</script>
<script>
    import { mapActions } from 'vuex';
    import * as bootstrap from "bootstrap/dist/js/bootstrap";
    import Accordion from 'accordion-js';
    import 'accordion-js/dist/accordion.min.css';
    
    export default {
        watch: {
            $route (to, from){
                this.setComponent({
                    value: to.params.view
                });
                
                const app = document.getElementById('app');
                app.tabIndex = '-1';
                app.focus();

                let offcanvas = document.getElementById('offcanvas'); 
                let bsOffcanvas = bootstrap.Offcanvas.getInstance(offcanvas);
                if (bsOffcanvas) {
                    bsOffcanvas.hide();
                }
            }
        },
        methods: {
            ...mapActions(['setComponent'])
        },
        mounted() {
            const urlParams = new URLSearchParams(window.location.search);
            const initIndex = parseInt(urlParams.get('init'));
            new Accordion('.accordion-container', {
                openOnInit: [initIndex],
                showMultiple: true
            });
            new Accordion('.accordion-container-child', {
                openOnInit: [initIndex],
                showMultiple: true
            });
        },
    }
</script>
<style scoped>
    .icon{
        font-size: 20px;
        /* font-weight: bold; */
        color: white;
    }

    .sub-menu{
        font-size: 11.9px;
        margin-left: 15px;
    }

    .main-menu{
        font-size: 13px;
        font-weight: normal;
        font-family: 'Inter-Light' !important;
    }
    .parent{
        background-color: unset;
        border: unset;
        font-family: 'Inter-Light' !important;   
        padding-left: 10px;
    }
    nav {
        padding: 10px 15px;
        /* background-color: #002316; */
        background-color: #0B0724;
        height: 650px;
        border-radius: 5px;
    }
    nav ul{
        font-size: 14px;
        margin-left: -12px;
    }

    nav a{
        color: white;
        margin-left: 0.5em;
        font-family: 'Inter-Light' !important;
        font-size: 12px;
    }

    nav a:focus{
        color: #BAAFFF;
    }

    nav .btn::before {
        width: 2em;
    }
    nav a:hover,
    nav button:hover,
    nav button:focus { /* Sidebar Menu Hover */
        /* color: #63ff43 !important; */
        color: #BAAFFF!important;
        background-color: unset;
        font-weight: bold;
    }
    nav .btn:focus {
        box-shadow: unset;
    }
    nav .btn::before {
        transform-origin: 0.9em 50%;
    }

    nav .btn{
        color: white;
    }

    nav .btn[aria-expanded="true"] {
        color: white;
    }

    nav .btn::before {
        width: 2em;
        color: white;
        content:none;
    }
    
    .mb-1{
        font-size: 13px;
    }

    a.router-link-active.router-link-exact-active {
        color: #BAAFFF;
        font-weight: bold;
    }

    /* Style the buttons that are used to open and close the accordion panel */
    .ac {
        margin-top: unset;
        border: unset;
        background-color: transparent;
        box-sizing: unset;
    }
    .ac .ac-trigger {
        font: inherit;
        font-family: Arial, Helvetica, sans-serif;
        color: #fff;
        font-size: 15px;
        font-weight: normal;
        line-height: 1.5em;
    }
    .ac .ac-trigger::after {
        content: "+";
        right: 0px;
        left: -8px;
    }

    .ac .ac-trigger-child {
        font: inherit;
        font-family: Arial, Helvetica, sans-serif;
        color: #fff;
        font-size: 15px;
        font-weight: normal;
        line-height: 1.5em;
    }
    .ac .ac-trigger-child::after {
        content: "+";
        right: 0px;
        left: -8px;
    }
</style>