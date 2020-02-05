<template>
    <nb-container>
        <nb-header :style="{height:80,paddingTop:25}">
            <nb-left>
                <nb-button transparent :on-press="go_back">
                    <nb-icon name="arrow-back"/>
                </nb-button>
            </nb-left>
            <nb-body>
                <nb-title>The Hacker</nb-title>
            </nb-body>
            <nb-right/>
        </nb-header>

        <nb-content :contentContainerStyle="{paddingTop:5}">

            <nb-grid :style="{padding:10}">
                <nb-row>
                    <nb-col>
                        <nb-card no-shadow transparent>
                            <nb-card-item :style="{paddingBottom:0,paddingTop:0,paddingLeft:0,paddingRight:0}">
                                <nb-body>
                                    <image :style="{width:'100%',height: 200}"
                                           :source="require('../../assets/pizza.jpg')"
                                           class="card-item-image"/>
                                    <nb-text
                                            :style="{marginBottom:0,paddingTop:8,paddingBottom:8,marginLeft:0,fontWeight:'bold',color:'grey'}">
                                        Pizza
                                    </nb-text>
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

            <nb-list-item :style="{paddingRight:14}" transparent no-shadow avatar>
                <nb-left>
                    <nb-thumbnail small :source="require('../../assets/user.jpg')"/>
                </nb-left>
                <nb-body>
                    <nb-text>Mayur Patel</nb-Text>
                    <nb-form :style="{width:'100%',marginTop:8}">
<!--                    <nb-item rounded>-->
                      <nb-textarea :rowSpan="3" :style="{paddingTop:8}" bordered placeholder="Your comment..." />
<!--                    </nb-item>-->
                        <nb-button :style="{width:60,marginTop: 9}" small>
                            <nb-text>Add</nb-text>
                        </nb-button>
                  </nb-form>
                </nb-body>
            </nb-list-item>
            <nb-list-item :style="{paddingRight:14}" avatar>
                <nb-left>
                    <nb-thumbnail small :source="require('../../assets/user.jpg')"/>
                </nb-left>
                <nb-body>
                    <nb-text>Mayur Patel</nb-Text>
                    <nb-text note>Doing what you like will always keep you happy.....</nb-Text>
                </nb-body>
                <nb-right>
                    <nb-text note>3:43 pm</nb-text>
                </nb-right>
            </nb-list-item>
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
                <nb-button :on-press="go_profile">
                    <nb-icon name="contact"/>
                    <nb-text>Mayur</nb-text>
                </nb-button>
            </nb-footer-tab>
        </nb-footer>

    </nb-container>
</template>

<script>
    import React from "react";
    import Vue from "vue-native-core";
    import {TabHeading, Icon, Text} from "native-base";
    import {VueNativeBase} from "native-base";
    import * as Permissions from 'expo-permissions'
    import * as ImagePicker from 'expo-image-picker'

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
                selected_image_data: '',
                selected_image_type: ''
            };
        },
        methods: {
            go_profile() {
                this.navigation.navigate("User");
            },
            go_map() {
                this.navigation.navigate("MapView");
            },
            go_home() {
                this.navigation.navigate("Home");
            },
            go_post() {
                this.navigation.navigate("PostItem");
            },
            go_back() {
                this.navigation.goBack();
            },
            async upload_pic() {
                const permis_obj = await Permissions.askAsync(Permissions.CAMERA_ROLL);

                if (permis_obj.status === 'granted') {
                    let pickerResult = await ImagePicker.launchImageLibraryAsync({
                        allowsEditing: false,
                        base64: true,
                        // aspect: [4, 3],
                    });

                    this.selected_image_data = pickerResult.base64;

                    console.log(this.selected_image_data);
                    // this._handleImagePicked(pickerResult);

                    if (!pickerResult.cancelled) {
                        // uploadResponse = await uploadImageAsync(pickerResult.uri);

                        // ImagePicker saves the taken photo to disk and returns a local URI to it
                        let localUri = pickerResult.uri;
                        let filename = localUri.split('/').pop();

                        // Infer the type of the image
                        let match = /\.(\w+)$/.exec(filename);
                        let type = match ? `image/${match[1]}` : `image`;
                        this.selected_image_type = pickerResult.base64;

                        // Upload the image using the fetch and FormData APIs
                        let formData = new FormData();
                        // Assume "photo" is the name of the form field the server expects
                        formData.append('photo', {uri: localUri, name: filename, type});

                        // console.log(formData);

                        // uploadResult = await uploadResponse.json();

                        // this.setState({
                        //   image: uploadResult.location
                        // });
                    }
                }
            },
            getHeadingCompForTab1: function () {
                return (
                    <TabHeading>
                        <Icon name="paper"/>
                        <Text>Your Posts</Text>
                    </TabHeading>
                );
            },
            getHeadingCompForTab2: function () {
                return (
                    <TabHeading>
                        <Icon name="heart"/>
                        <Text>Favourites</Text>
                    </TabHeading>
                );
            }
        }
    };
</script>
