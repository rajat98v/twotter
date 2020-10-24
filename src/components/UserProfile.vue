<template>
    <div class="user-profile">
        <div class="user-profile_user-panel">
            <h1 class="user-profile_username">@{{ user.username }}</h1>
            <div class="user-profile_admin-badge" v-if="user.isAdmin">
                Admin
            </div>
            <div class="user-profile_follower-count">
                <strong>Followers: </strong> {{ followers }}
            </div>
            <div>
                <form class="user-profile_create-twoot" @submit.prevent="createNewTwoot">
                    <label for="newTwoot"><strong>New Twoot</strong></label> <!-- Labels Necessary for form -->
                    <textarea id="newTwoot" rows="4" v-model="newTwootContent"></textarea>

                    <div class="user-profile_create-twoot-type">
                        <label for="newTwootType"><strong>Type: </strong></label>
                        <select id="newTwootType" v-model="selectedTwootType">
                            <option :value="option.value" v-for="(option, index) in twootType" :key="index">
                                {{option.name}}

                            </option>
                        </select>

                    </div>
                    <button>
                        Twoot!
                    </button>
                </form>
            </div>
        </div>
        <div class="user-profile_twoots-wraps">
            <TwootItem
                v-for="twoot in user.twoots"
                :key="twoot.id"
                :username="user.username"
                :twoot="twoot"
                @favourite="toggleFavourite"
            />
        </div>
    </div>
</template>

<script>
import TwootItem from "./TwootItem";

export default {
    name: "UserProfile",
    components: { TwootItem },
    data() {
        return {
            followers: 0,
            newTwootContent: '',
            selectedTwootType: 'instance', // Making default empty
            twootType: [
                {value: 'draft', name: 'Draft'},
                {value: 'instance', name: 'Instance Twoot'},
            ],
            user: {
                id: 1,
                username: "_RajatVerma",
                firstname: "Rajat",
                lastname: "Verma",
                email: "rajatv89@gmail.com",
                isAdmin: true,
                twoots: [
                    {
                        id: 1,
                        content: "Twotter is amazing!"
                    },
                    {
                        id: 2,
                        content:
                            "Don't forget to check out my projects on github!"
                    }
                ]
            }
        };
    },
    watch: {
        followers(newFollowerCount, oldFollowerCount) {
            if (oldFollowerCount < newFollowerCount) {
                console.log(`${this.user.username} has gained a follower!`);
            }
        }
    },
    computed: {
        fullname() {
            return `${this.user.firstname} ${this.user.lastname}`; // String Literals
            // Eqivalent to this.user.firstname+" "+this.user.lastname
        }
    },
    methods: {
        followUser() {
            this.followers++;
        },
        toggleFavourite(id) {
            console.log(`Favourite tweet #${id}`)
        },
        createNewTwoot() {
            if (this.newTwootContent && this.selectedTwootType !== 'draft') {
                this.user.twoots.unshift({ // adds at the begining of list
                    id: this.user.twoots.length + 1,
                    content: this.newTwootContent,
                })
                this.newTwootContent = '';

            }
        }
    },
    mounted() {
        this.followUser();
    }
};
</script>

<style>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%;
}
.user-profile_user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;
}
.user-profile_admin-badge {
    background: rebeccapurple;
    color: white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 10px;
    font-weight: bold;
}
.user-profile_create-twoot {
    padding-top: 20px;
    display: flex;
    flex-direction: column;
}

h1 {
    margin: 0;
}
</style>
