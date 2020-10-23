<template>
    <div id="app">
        @{{ user.username}} - {{ fullname}}
        <strong>Followers </strong> {{ followers }}
        <button @click="followUser">
            Follow
        </button>
    </div>
</template>

<script>
export default {
    name: "App",
    data() {
        return {
            followers: 0,
            user: {
                id: 1,
                username: '_RajatVerma',
                firstname: 'Rajat',
                lastname: 'Verma',
                email: 'rajatv89@gmail.com',
                isAdmin: true,
            }
        }
    },
    watch: {
        followers(newFollowerCount, oldFollowerCount) {
            if (oldFollowerCount < newFollowerCount) {
                console.log(`${ this.user.username } has gained a follower!`)
            }
        }
    },
    computed: {
        fullname() {
            return `${this.user.firstname} ${this.user.lastname}` // String Literals
            // Eqivalent to this.user.firstname+" "+this.user.lastname
        }
    },
    methods: {
        followUser() {
            this.followers++
        }
    },
    mounted() {
        this.followUser();
    }

};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    display: flex;
    flex-direction: column;
    text-align: center;
}
</style>
