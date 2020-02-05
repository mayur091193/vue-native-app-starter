<template>
    <nb-container>
        <nb-header :style="{height:80,paddingTop:25}">
            <nb-left>
                <nb-button transparent :on-press="go_back">
                    <nb-icon name="arrow-back"/>
                </nb-button>
            </nb-left>
            <nb-body>
                <nb-title>Nearby</nb-title>
            </nb-body>
            <nb-right/>
        </nb-header>
        <view class="container">
            <map-view class="container"
                      :initial-region="coordinates">
                <Marker
                        :coordinate="coordinates"
                        title="City Vista"
                >
                  <image :style="{width:220,height: 220}"
                                           :source="require('../../assets/coming_soon.png')"
                                           class="card-item-image"/>
                </Marker>
            </map-view>
        </view>
        <nb-footer>
            <nb-footer-tab>
                <nb-button :on-press="go_home">
                    <nb-icon name="apps"/>
                    <nb-text>Hacker</nb-text>
                </nb-button>
                <nb-button :active="true">
                    <nb-icon name="bicycle"/>
                    <nb-text>Nearby</nb-text>
                </nb-button>
                <nb-button :on-press="go_post">
                    <nb-icon name="paper"/>
                    <nb-text>Post</nb-text>
                </nb-button>
                <nb-button :on-press="go_profile">
                    <nb-icon name="contact"/>
                    <nb-text>Mayur</nb-text>
                </nb-button>
            </nb-footer-tab>
        </nb-footer>
    </nb-container>
</template>

<script>
    import MapView from 'react-native-maps';
    import {Marker} from 'react-native-maps';
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
                coordinates: {
                    latitude: 18.561111,
                    longitude: 73.944854,
                    latitudeDelta: 0.0922,
                    longitudeDelta: 0.0421
                }
            };
        },
        components: {
            MapView, Marker
        },
        methods: {
            go_home() {
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
            go_profile() {
                this.navigation.navigate("User");
            },
            go_post() {
                this.navigation.navigate("PostItem");
            }
        }
    };
</script>
<style>
    .container {
        flex: 1;
    }
</style>