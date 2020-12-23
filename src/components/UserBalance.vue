<template>
    <div id="UserBalance" class="user_balance">
        <h2> {{username}}</h2>
        <h2>Tu saldo es: <span>  {{balance}} COP </span> </h2>
        <table>
            <tr>
                <td>Primer nombre:</td>
                <td>{{userData.per_cre_nombre1}}</td>
            </tr>
            <tr>
                <td>Segundo nombre:</td>
                <td>{{userData.per_cre_nombre2}}</td>
            </tr>
            <tr>
                <td>Primer apellido:</td>
                <td>{{userData.per_cre_apellido1}}</td>
            </tr>
            <tr>
                <td>Segundo apellido:</td>
                <td>{{userData.per_cre_apellido2}}</td>
            </tr>
        </table>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'UserBalance',
    data: function (){
        return {
            id: 0,
            userData: {}
        }
    },

    created: function(){
        this.id = this.$route.params.id

        let self = this
        axios.get("http://cicle3sprint4unal.herokuapp.com/user/" + this.id).then((result) => {
            self.userData = result.data
        })
    }
}
</script>


<style>
    #UserBalance{
        width: 100%;
        height: 100%;

        display: flex;
        flex-direction: column;
        justify-content: center;    
        align-items: center;
    }

    #UserBalance h2{
        font-size: 50px;
        color: #283747;
    }

    #UserBalance span{
        color: crimson;
        font-weight: bold;
    }
</style>