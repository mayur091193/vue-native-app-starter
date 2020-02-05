<template>
    <nb-container v-if="isLoaded">
        <app-navigator></app-navigator>
    </nb-container>
</template>

<script>
    import {
        createAppContainer,
        createStackNavigator,
    } from "vue-native-router";

    import LoginScreen from "./screen/login.vue";
    import HomeScreen from "./screen/home.vue";
    import UserScreen from "./screen/user.vue";
    import SignUpScreen from "./screen/sign_up.vue";
    import MapViewScreen from "./screen/map_view.vue";
    import PostItemScreen from "./screen/post_item.vue";
    import ItemDetailsScreen from "./screen/item_details.vue";

    import * as Font from 'expo-font';

    const StackNavigator = createStackNavigator(
        {
            Home: HomeScreen,
            Login: LoginScreen,
            User: UserScreen,
            SignUp: SignUpScreen,
            MapView: MapViewScreen,
            PostItem: PostItemScreen,
            ItemDetails: ItemDetailsScreen
        },
        {
            initialRouteName: 'Login',
            headerMode: "none"
        }
    );

    const AppNavigator = createAppContainer(StackNavigator);

    export default {
        components: {AppNavigator},
        data: function () {
            return {
                isLoaded: false
            };
        },
        async mounted() {
            await Font.loadAsync({
                'Roboto_medium': require('../node_modules/native-base/Fonts/Roboto_medium.ttf'),
            });

            this.isLoaded = true;
            console.log("Loaded");
        }
    }
</script>