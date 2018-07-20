<template>
    <b-container>
        <br/>
        <form class="shadow-lg p-3 ">
            <div role="group">
                <label for="inputLive">Name:</label>
                <b-form-input id="inputLive" v-on:keypress="submit" v-model.trim="user.name" type="text" :state="nameState" aria-describedby="inputLiveHelp inputLiveFeedback" placeholder="Enter your name"></b-form-input>
                <b-form-invalid-feedback id="inputLiveFeedback">
                    Name should be minimum of 3 character
                </b-form-invalid-feedback><br/>
            </div>
            <div>
                <label>Date:</label>
                <b-form-input type="date" v-model="user.date"></b-form-input><br/>
            </div>
            <div>
                <label>Time:</label>
                <b-form-input type="time" v-model="user.time"></b-form-input><br/>
            </div>
            <button type="cancel" class="btn">Cancel</button>
            <button type="submit" class="btn btn-primary" v-on:click="submit">Submit</button>
        </form>
    </b-container>
</template>

<script>
    export default {
        name: "Form",
        data: function() {
            return {
                users: [],
                user: {
                    name: "",
                    date: "",
                    time: ""
                }
            };
        },
        computed: {
            nameState() {
                return this.user.name.length > 2 ? true : false;
            }
        },
        props: {
            userObject:{
                type: Object,
            }
        },
        methods: {
            submit: function() {
               this.$emit("submit-item", this.users.push({
                    id: ++this.userCount,
                    name: this.user.name,
                    date: this.user.date,
                    time: this.user.time
                })
               )
                alert("form submitted");
                this.user = {
                    name: "",
                    date: "",
                    time: ""
                };
                // eslint-disable-next-line
                console.log(this.user);
                
            }
        }
    };
</script>


<style>
    label {
        float: left;
        font-size: 20px;
        font-weight: bold;
    }
    
    form {
        background: #F5F5F5;
    }
    
    .btn {
        margin-right: 25px;
    }
</style>