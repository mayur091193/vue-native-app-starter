<template>
    <nb-container>
        <nb-header :style="{height:80,paddingTop:25}">
            <nb-left>
                <nb-button transparent :on-press="go_back">
                    <nb-icon name="arrow-back"/>
                </nb-button>
            </nb-left>
            <nb-body>
                <nb-title>Post</nb-title>
            </nb-body>
            <nb-right/>
        </nb-header>

        <nb-content :contentContainerStyle="{paddingTop:5}">
            <!--            :contentContainerStyle="{justifyContent: 'center',alignItems: 'center',flex: 1}" padder-->
            <view :style="{justifyContent: 'center',alignItems: 'center'}">
                <image
                        :source="require('../../assets/icon.png')"
                        :style="{width: 60, height: 60}"
                >
                </image>
            </view>

            <view :style="{width:'100%',padding:10,marginTop:-14}">
                <nb-form :style="{paddingRight:17}">
                    <nb-item stackedLabel>
                        <nb-input placeholder="Title"/>
                    </nb-item>
                    <nb-item stackedLabel>
                        <nb-input placeholder="Description"/>
                    </nb-item>
                </nb-form>
                <nb-button :on-press="upload_pic" :style="{width:170,marginTop:25,marginLeft:12}" small iconLeft>
                    <nb-icon active name="home"/>
                    <nb-text>Upload image</nb-text>
                </nb-button>
                <image v-if="selected_image_data"
                       :source="{uri: 'data:'+selected_image_type+';base64,'+selected_image_data}"
                       :style="{width: 150, height: 150, marginTop:25,marginLeft:12}"
                >
                </image>
                <nb-button :style="{marginTop:25}" block dark>
                    <nb-text>post</nb-text>
                </nb-button>


            </view>

            <nb-tabs :style="{marginTop:15}">
              <nb-tab :heading="getHeadingCompForTab1()">
                  <nb-grid :style="{padding:10}">
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
            </nb-grid>
              </nb-tab>
              <nb-tab :heading="getHeadingCompForTab2()">
                <nb-text :style="{color:'grey',fontWeight:'bold',fontSize:14,padding:15}">No favourites till now...Go make some!!</nb-text>
              </nb-tab>
            </nb-tabs>

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
                <nb-button :active="true">
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
    import { TabHeading, Icon, Text } from "native-base";
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
            getHeadingCompForTab1: function() {
              return (
                <TabHeading>
                  <Icon name="paper" />
                  <Text>Your Posts</Text>
                </TabHeading>
              );
            },
            getHeadingCompForTab2: function() {
              return (
                <TabHeading>
                  <Icon name="heart" />
                  <Text>Favourites</Text>
                </TabHeading>
              );
            }
        }
    };
</script>
