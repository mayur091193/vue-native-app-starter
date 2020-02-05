<template>
    <nb-container>
        <nb-header searchBar rounded :style="{height:80,paddingTop:25}">
            <nb-item>
                <nb-icon active name="search"/>
                <nb-input placeholder="Search"/>
                <nb-icon active name="wine"/>
            </nb-item>
            <nb-button transparent>
                <nb-text>Search</nb-text>
            </nb-button>
        </nb-header>

        <nb-content padder>
            <nb-grid>
                <nb-row>
                    <nb-col>
                        <nb-card>
                            <nb-card-item :style="{paddingLeft:5}" bordered>
                                <nb-left>
                                    <nb-body>
                                        <nb-text :style="{fontWeight:'bold',color:'grey'}">The Hacker</nb-text>
                                    </nb-body>
                                </nb-left>
                                <nb-right>
                                   <nb-text :style="{color:'grey'}">11h ago</nb-text>
                                </nb-right>
                            </nb-card-item>
                            <nb-card-item :style="{paddingBottom:0,paddingTop:0,paddingLeft:0,paddingRight:0}">
                                <nb-body>
                                    <image :style="{width:'100%',height: 145}"
                                           :source="require('../../assets/pizza.jpg')"
                                           class="card-item-image"/>
                                    <nb-text :style="{marginBottom:0,paddingTop:8,paddingBottom:8,marginLeft:15,fontWeight:'bold',color:'grey'}">Pizza</nb-text>
                                </nb-body>
                            </nb-card-item>
                            <nb-card-item footer bordered :style="{paddingTop: 0,paddingLeft:18,paddingBottom:0}">
                                <nb-left>
                                    <nb-button transparent>
                                        <nb-icon name="thumbs-up"></nb-icon>
                                        <nb-text :style="{paddingLeft:4}">9</nb-text>
                                    </nb-button>
                                    <nb-button transparent>
                                        <nb-icon name="chatbubbles"></nb-icon>
                                        <nb-text :style="{paddingLeft:4}">18</nb-text>
                                    </nb-button>
                                    <nb-button transparent>
                                        <nb-icon name="star" :style="{color:'#ccb20a'}"></nb-icon>
                                        <nb-text :style="{paddingLeft:4,color:'#ccb20a'}">4.5</nb-text>
                                    </nb-button>
                                </nb-left>
                                <nb-right>
                                     <nb-button transparent>
                                        <nb-icon name="person" :style="{marginRight:0,color:'grey'}"></nb-icon>
                                        <nb-text :style="{paddingRight:0,paddingLeft:7,color:'grey'}">Mayur</nb-text>
                                    </nb-button>
                                </nb-right>
                            </nb-card-item>
                        </nb-card>
                    </nb-col>
                </nb-row>
                <nb-row :on-press="go_item_details_view">
                    <nb-col>
                        <nb-card>
                            <nb-card-item :style="{paddingLeft:5}" bordered>
                                <nb-left>
                                    <nb-body>
                                        <nb-text :style="{fontWeight:'bold',color:'grey'}">The Hacker</nb-text>
                                    </nb-body>
                                </nb-left>
                                <nb-right>
                                   <nb-text :style="{color:'grey'}">11h ago</nb-text>
                                </nb-right>
                            </nb-card-item>
                            <nb-card-item :style="{paddingBottom:0,paddingTop:0,paddingLeft:0,paddingRight:0}">
                                <nb-body>
                                    <image :style="{width:'100%',height: 145}"
                                           :source="require('../../assets/pizza.jpg')"
                                           class="card-item-image"/>
                                    <nb-text :style="{marginBottom:0,paddingTop:8,paddingBottom:8,marginLeft:15,fontWeight:'bold',color:'grey'}">Pizza</nb-text>
                                </nb-body>
                            </nb-card-item>
                            <nb-card-item footer bordered :style="{paddingTop: 0,paddingLeft:18,paddingBottom:0}">
                                <nb-left>
                                    <nb-button transparent>
                                        <nb-icon name="thumbs-up"></nb-icon>
                                        <nb-text :style="{paddingLeft:4}">9</nb-text>
                                    </nb-button>
                                    <nb-button transparent>
                                        <nb-icon name="chatbubbles"></nb-icon>
                                        <nb-text :style="{paddingLeft:4}">18</nb-text>
                                    </nb-button>
                                    <nb-button transparent>
                                        <nb-icon name="star" :style="{color:'#ccb20a'}"></nb-icon>
                                        <nb-text :style="{paddingLeft:4,color:'#ccb20a'}">4.5</nb-text>
                                    </nb-button>
                                </nb-left>
                                <nb-right>
                                     <nb-button transparent>
                                        <nb-icon name="person" :style="{marginRight:0,color:'grey'}"></nb-icon>
                                        <nb-text :style="{paddingRight:0,paddingLeft:7,color:'grey'}">Mayur</nb-text>
                                    </nb-button>
                                </nb-right>
                            </nb-card-item>
                        </nb-card>
                    </nb-col>
                </nb-row>
            </nb-grid>

        </nb-content>

        <nb-footer>
            <nb-footer-tab>
                <nb-button :active="true">
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
                <nb-button :on-press="go_profile">
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
            go_profile() {
                this.navigation.navigate("User");
            },
            go_map() {
                this.navigation.navigate("MapView");
            },
            go_item_details_view() {
                this.navigation.navigate("ItemDetails");
            },
            go_post() {
                this.navigation.navigate("PostItem");
            }
        }
    };
</script>
