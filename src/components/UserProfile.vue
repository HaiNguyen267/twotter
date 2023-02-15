<template>
    <div class="user-profile">
        <div class="user-profile__user-panel">
            <h1 class="user-profile__username">@{{ user.username }}</h1>
            <div class="user-profile__admin-badge" v-if="user.isAdmin">
                Admin
            </div>
            <div class="user-profile__user-bagde" v-else>
                User
            </div>
            <div class="user-profle__follower-count">
                <strong>Followers: </strong> {{ followers }}
            </div>

            <CreateTwootPanel @add-twoot="addTwoot"/>
        </div>



        <div class="user-profile__twoots-wrapper">
            <TwootItem class="user-profile__twoot" v-for="(twoot, index) in user.twoots" :key="index" :twoot="twoot"
                :username="user.username" @favorite="toggleFavorite" />
        </div>
    </div>
</template>

<script>
import TwootItem from './TwootItem.vue'
import CreateTwootPanel from './CreateTwootPanel.vue';
export default {
    name: 'UserProfile',
    components: { CreateTwootPanel, TwootItem },
    data() {
        return {
            render: 0,
            isLoading: false,
            followers: 1,
            message: '',
            user: {
                id: 1,
                username: '_MitchellRomney',
                firstName: "Mitchell Roe",
                lastName: "Romney",
                email: 'MitchelRomney@theearthissquare.com',
                isAdmin: false,
                twoots: [
                    { id: 1, content: 'Twooter is amazing' },
                    { id: 2, content: "Don't forget to subscribe to The Earth is Square!" }
                ]
            }

        }
    },
    watch: {
        followers(newFollowCount, oldFollowCount) {
            if (newFollowCount > oldFollowCount) {
                console.log(`${this.user.username} has gained a follower`);
                this.message = "A new follower has followed you!"
            } else {
                this.message = "You lose a follower!"
            }
        }
    },
    computed: {
        fullName() {
            return `${this.user.firstName} ${this.user.lastName}`
        },
        newTwootCharacterCount() {
            return this.newTwootContent.length
        }
    },
    methods: {
        followUser() {
            this.followers++;
        },
        incrementRender() {
            this.render++;
        },
        unfollowUser() {
            if (this.followers > 0) {
                this.followers--;
            }
        },
        toggleFavorite(id) {
            console.log(`favorited twoot #${id}`);


        },
        mounted() {
            this.incrementRender()
        },
        addTwoot(content) {
            this.user.twoots.unshift({
                id: this.user.twoots.length + 1,
                content: content
            })
        }
    }
}
</script>

<style lang="scss" scoped>
.user-profile {
    display: flex;

    .user-profile__user-panel {
        font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
        padding: 15px 20px;
        text-align: left;
        height: fit-content;
        width: fit-content;
        background: white;
        border-radius: 10px;

        .user-profile__username {
            margin-bottom: 10px;
        }


        .user-profile__admin-badge {
            color: white;
            background: rgb(118, 9, 118);
            border-radius: 5px;
            width: fit-content;
            padding: 5px 10px;
        }

        .user-profile__user-bagde {
            color: white;
            background: rgb(12, 175, 72);
            border-radius: 5px;
            width: fit-content;
            padding: 5px 10px;
        }


        
    }

    .user-profile__twoots-wrapper {
        padding: 0 50px;
    }

}









</style>
