<template>
    <nb-container>
        <nb-header :style="{height:80,paddingTop:25}">
            <nb-left>
                <nb-button transparent :on-press="go_back">
                    <nb-icon name="arrow-back"/>
                </nb-button>
            </nb-left>
            <nb-body>
                <nb-title>Profile</nb-title>
            </nb-body>
            <nb-right/>
        </nb-header>
        <nb-content padder>
            <nb-list-item thumbnail>
                <nb-left>
                    <nb-thumbnail square :source="require('../../assets/user.jpg')"/>
                </nb-left>
                <nb-body>
                    <nb-text :style="{fontWeight:'bold'}">Mayur Patel</nb-Text>
                    <nb-text note :numberOfLines="1">Its time to build a difference . .</nb-Text>

                </nb-body>
            </nb-list-item>

            <nb-label :style="{padding:10,marginTop:10}">
                <nb-icon :style="{fontSize:15}" active name="person"/>
                <nb-text :style="{fontSize:15,color:'grey',fontWeight:'bold'}">&nbsp;&nbsp; mayur091193@gmail.com</nb-text>
            </nb-label>
            <nb-label :style="{padding:10}">
                <nb-icon :style="{fontSize:15}" active name="person"/>
                <nb-text :style="{fontSize:15,color:'grey',fontWeight:'bold'}">&nbsp;&nbsp; 9724663992</nb-text>
            </nb-label>
            <nb-label :style="{padding:10}">
                <nb-icon :style="{fontSize:15}" active name="speedometer"/>
                <nb-text :style="{fontSize:15,color:'grey',fontWeight:'bold'}">&nbsp;&nbsp; Member for 4 years, 6 months</nb-text>
            </nb-label>
            <nb-label :style="{padding:10}">
                <nb-icon :style="{fontSize:15}" active name="eye"/>
                <nb-text :style="{fontSize:15,color:'grey',fontWeight:'bold'}">&nbsp;&nbsp; 18 profile views</nb-text>
            </nb-label>
            <nb-button :style="{marginTop:10}" small block dark>
                <nb-text>Edit Profile</nb-text>
            </nb-button>
            <nb-button :on-press="log_out" :style="{marginTop:20}" small block danger>
                <nb-text>Logout</nb-text>
            </nb-button>
        </nb-content>

        <nb-footer>
            <nb-footer-tab>
                <nb-button :on-press="go_home">
                    <nb-icon name="apps"/>
                    <nb-text>Hacker</nb-text>
                </nb-button>
                <nb-button :on-press="go_map">
                    <nb-icon name="bicycle"/>
                    <nb-text>Nearby</nb-text>
                </nb-button>
                <nb-button :on-press="go_post">
                    <nb-icon name="paper"/>
                    <nb-text>Post</nb-text>
                </nb-button>
                <nb-button :active="true">
                    <nb-icon name="contact"/>
                    <nb-text>Mayur</nb-text>
                </nb-button>
            </nb-footer-tab>
        </nb-footer>

    </nb-container>
</template>

<script>
    import Vue from "vue-native-core";
    import {VueNativeBase} from "native-base";

    // registering all native-base components to the global scope of the Vue
    Vue.use(VueNativeBase);

    export default {
        props: {
            navigation: {
                type: Object
            }
        },
        data: function () {
            return {

            };
        },
        methods: {
            go_home(){
                this.navigation.navigate("Home");
            },
            go_back() {
                this.navigation.goBack();
            },
            log_out() {
                this.navigation.navigate("Login");
            },
            go_map() {
                this.navigation.navigate("MapView");
            },
            go_post() {
                this.navigation.navigate("PostItem");
            }
        }
    };
</script>
