<template>
        <!--        <nb-header :style="{height:80,paddingTop:25}">-->
        <!--            <nb-left>-->
        <!--                <nb-button transparent>-->
        <!--                    <nb-icon name="menu"/>-->
        <!--                </nb-button>-->
        <!--            </nb-left>-->
        <!--            <nb-body>-->
        <!--                <nb-title>Header</nb-title>-->
        <!--            </nb-body>-->
        <!--            <nb-right/>-->
        <!--        </nb-header>-->
        <nb-content :contentContainerStyle="{justifyContent: 'center',alignItems: 'center',flex: 1}" padder>
            <!--            :contentContainerStyle="{justifyContent: 'center',alignItems: 'center',flex: 1}" padder-->
            <view :style="{justifyContent: 'center',alignItems: 'center'}">
                <image
                        :source="require('../../assets/icon.png')"
                        :style="{width: 150, height: 150}"
                >
                </image>
                <nb-label :style="{width:115,fontSize:20,marginTop: 20,fontWeight:'bold'}">The Hacker</nb-label>
            </view>

            <view :style="{width:'100%',padding:10,marginTop:-14}">
                <nb-form :style="{paddingRight:17}">
                    <nb-item stackedLabel>
                        <nb-input placeholder="Email"/>
                    </nb-item>
                    <nb-item stackedLabel>
                        <nb-input placeholder="Password"/>
                    </nb-item>
                </nb-form>
                <nb-button :on-press="sign_in" :style="{marginTop:25}" block dark>
                    <nb-text>LOGIN</nb-text>
                </nb-button>
                <nb-label :style="{fontSize:15,marginTop: 25}">Don't have an account?
                    <nb-text :on-press="sign_up" :style="{color:'blue',fontWeight:'bold'}">Create One</nb-text>
                </nb-label>


            </view>

        </nb-content>
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
                isLoaded: false
            };
        },
        methods: {
            sign_in() {
                this.navigation.navigate("Home");
            },
            sign_up() {
                this.navigation.navigate("SignUp");
            }
        }
    };
</script>