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
        </div>
        <div class="user-profile_twoots-wrapper">
            <div class="user-profile_twoots" v-for="twoot in user.twoots" :key="twoot.id" >
                {{ twoot.content }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "UserProfile",
    data() {
        return {
            followers: 0,
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
                        content: "Don't forget to check out my projects on github!"
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

h1 {
    margin: 0;
}
</style>
